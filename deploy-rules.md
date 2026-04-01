# Deploy Rules — cyberdub-ai Server

## CRITICAL: Read before generating any deployment code

This website runs on a home server (cyberdub-ai, Ubuntu 24.04). 
These rules are MANDATORY. Do not invent alternatives.

---

## Architecture

```
Internet → Caddy (ports 80/443) → Docker containers (internal network)
```

- **Reverse proxy: CADDY ONLY.** Never nginx, never Apache, never any other proxy.
- **All services run in Docker** via `docker-compose.yml`.
- Caddy and all web containers share the Docker network: **`n8n_net`** (external network, already exists).

---

## Existing setup for cyberdub.su

The site already has a container and Caddy block configured:

| Component | Value |
|-----------|-------|
| Container name | `cyberdub-website` |
| Internal port | `3056` |
| Docker network | `n8n_net` |
| Compose file | `~/stack/cyberdub-website/docker-compose.yml` |
| Caddy config | `~/stack/n8n/Caddyfile` |

**Caddy already routes `cyberdub.su` → `cyberdub-website:3056`.**
Do not create a new container with a different name or port.
Do not add a new Caddy block for `cyberdub.su` — it already exists.

---

## docker-compose.yml template for cyberdub-website

```yaml
services:
  cyberdub-website:
    build: .          # or image: cyberdub-website:latest
    container_name: cyberdub-website
    restart: unless-stopped
    expose:
      - "3056"        # internal only — Caddy proxies this
    networks:
      - n8n_net

networks:
  n8n_net:
    external: true
    name: n8n_net
```

Rules:
- Use `expose:` (internal only), NOT `ports:` (which opens to host)
- Always attach to `n8n_net`
- No secrets in docker-compose.yml — use `env_file: /srv/secrets/cyberdub-website.env`

---

## Occupied ports — DO NOT use these

```
80, 443          → Caddy (HTTP/HTTPS)
11434            → Ollama (LLM)
6333             → Qdrant (vector DB)
5678             → n8n (automation)
5432, 5433, 5435 → PostgreSQL instances
6379, 6382, 6385 → Redis instances
3000             → Grafana
9090             → Prometheus
3001             → Uptime Kuma
19999            → Netdata
8080             → OpenWebUI
3020–3025        → SNT-Pilot services
3040, 3070, 3075, 3080, 3096 → Other frontends
8050, 8070, 8072, 8090 → Other backends
3056             → cyberdub-website (current site)
1080             → SOCKS5 proxy (SSH tunnel to VPS)
8118, 8119       → Privoxy (HTTP proxy)
```

Before using any new port: run `docker ps` and `ss -tlnp` to verify it's free.

---

## Deployment commands

```bash
# Build and restart the site
cd ~/stack/cyberdub-website
docker compose build
docker compose up -d

# Reload Caddy config (after editing Caddyfile)
docker exec caddy caddy reload --config /etc/caddy/Caddyfile

# Check logs
docker compose logs -f --tail=50
```

---

## File structure rules

```
~/stack/cyberdub-website/     ← Docker Compose + Dockerfile here
  docker-compose.yml
  Dockerfile
  (source files or build context)

/srv/data/cyberdub-website/   ← persistent data (if any)
/srv/secrets/cyberdub-website.env  ← secrets (env vars, chmod 600)
~/stack/n8n/Caddyfile         ← reverse proxy config (single file for ALL domains)
```

---

## What NOT to do

- ❌ Do not install nginx or any other web server
- ❌ Do not use `ports:` in docker-compose (use `expose:` for internal services)
- ❌ Do not hardcode secrets in docker-compose.yml
- ❌ Do not add a second Caddy block for cyberdub.su (already exists)
- ❌ Do not create new Docker networks — attach to `n8n_net`
- ❌ Do not expose database ports to host (DBs stay internal)
- ❌ Do not run services with `docker run` directly — always use docker-compose.yml
