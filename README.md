A self-hosted infrastructure inventory and operations workspace for homelabs, small racks, network rooms, and lab environments. Bring racks, devices, ports, cables, Networks/IPAM, storage, Wi-Fi, compute, discovery, monitoring, documentation, images, integrations, reports, labs, and administration into one clean app.

## Features

- **Visual topology** — a movable React Flow network map with cable routes, health overlays, and rack/pyramid layouts
- **Racks, devices, ports & cables** — dense rack elevations, switch-panel port maps, and full cable patching
- **Networks and IPAM** — VLANs, subnets, DHCP zones and reservations, gateway/DNS protection, and multi-IP device records
- **Storage topology** — drive inventory, physical bays and enclosures, cross-device pools, missing members, and reusable templates
- **Monitoring** — per-device ICMP, TCP, HTTP/HTTPS, and SNMP health checks with email/Discord/Telegram alerting
- **Discovery** — IPAM-subnet, all-subnet, and manual-CIDR scanning with import reconciliation
- **Wi-Fi, compute & docs** — controller/SSID/AP/radio/client inventory, virtualization hosts, and markdown docs with images
- **Light & dark themes**, self-hosted fonts (works offline / air-gapped), and responsive mobile layout
- **OIDC sign-in** with per-provider role mapping (admin/editor/viewer)
- **Native SQLite** persistence with JSON export and native backup support

## Deploy

[![Deploy to Railway](https://railway.app/button.svg)](https://railway.com/deploy/rackpad)

One-click deploy provisions the Rackpad service and a `/data` volume for SQLite persistence.

## Configuration

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | Port the server listens on. Railway sets this automatically. | `3000` |
| `HOST` | Host address to bind. | `0.0.0.0` |
| `NODE_ENV` | Node environment. Keep `production`. | `production` |
| `DATABASE_PATH` | SQLite database file path. Backed by the `/data` volume. | `/data/rackpad.db` |
| `TRUST_PROXY` | Trust Railway reverse proxy headers. | `1` |
| `APP_URL` | Public URL for OIDC redirects and links. Auto-derived from Railway public domain. | `https://${{RAILWAY_PUBLIC_DOMAIN}}` |
| `OIDC_ENABLED` | Enable OIDC single sign-on. Configure OIDC_* vars before enabling. | `0` |

## Volumes

| Mount | Purpose |
|-------|---------|
| `/data` | SQLite database (`rackpad.db`) and native backup snapshots. Do not remove. |

## First Run

1. After deploy, open your public Railway URL.
2. Create the first admin account on initial page load.
3. Optionally configure OIDC via the Variables tab (`OIDC_ENABLED=1`, then set `OIDC_ISSUER_URL`, `OIDC_CLIENT_ID`, `OIDC_CLIENT_SECRET`, `OIDC_REDIRECT_URI`).
4. Navigate to Settings → Discovery to enable background network scanning.

## Tech Stack

- React + Vite frontend
- Fastify API
- SQLite (`better-sqlite3`) persistence
- Session-based authentication with admin/editor/viewer roles
- MIT licensed — [github.com/Kobii-git/rackpad](https://github.com/Kobii-git/rackpad)
