# Local n8n

Local n8n server with a Cloudflared tunnel for secure access from anywhere and webhook configuration.

One of the reasons for using a Cloudflared tunnel is to avoid exposing the IP address of my local network.

---

## Overview

This setup allows you to run an n8n instance locally while making it accessible through a secure Cloudflare Tunnel.  
It’s ideal for testing automations, webhooks, or integrations that require external access without deploying n8n to a public server.

By using Cloudflared, your local instance remains private — all traffic is routed through Cloudflare’s encrypted network, protecting your real IP and avoiding port forwarding or firewall changes.

---

## How It Works

1. **n8n Server:** Runs locally on your machine, handling workflows and automation logic.  
2. **Cloudflared Tunnel:** Creates a secure, outbound-only connection to Cloudflare’s network.  
3. **Public Endpoint:** Cloudflare assigns a unique URL that routes traffic to your local n8n instance.  
4. **Webhooks:** External services can trigger workflows using the public URL without exposing your local IP.

---

## Requirements

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)



## Run

1. **Install Requirements**  
   Make sure Docker and Docker Compose are installed on your system.

2. **Create a Tunnel Token in Cloudflared**  
   Generate a token from your Cloudflare dashboard to authenticate your tunnel.

3. **Set Environment Variables**  
   Create a `.env` file in the project root with the following values:

```bash
   DOMAIN_NAME={DOMAIN_NAME}       # The top-level domain to serve from
   SUBDOMAIN={SUBDOMAIN}           # The subdomain to serve from
   GENERIC_TIMEZONE=Europe/Madrid  # Timezone to set
   TUNNEL_TOKEN={tokennnnn}        # Cloudflared tunnel token
```
DOMAIN_NAME and SUBDOMAIN together determine where n8n will be reachable from.

4. Run docker compose
```bash
docker compose up -d
```

5. Check logs
```bash
docker n8n logs
docker cloudflared-tunnel logs
```

6. Access the Web Interface
Visit your configured domain or the URL provided by Cloudflare to access n8n.


## UPDATE NEW VERSIONS

1. Pull the Latest Version
```bash
docker compose pull
```

2. Stop and Remove the Old Version
```bash
docker compose down
```

3. Start the Updated Container
```bash
docker compose up -d
```
