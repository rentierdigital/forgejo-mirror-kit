# Forgejo Mirror Kit

Pull-only GitHub mirror on Forgejo. Docker kit, 5-minute setup.

> **Caveat:** This is a pull-only mirror. It syncs your code (branches, tags, commits) but not GitHub Issues, Actions, Packages, or settings. It's a safety net for your source code, not a full backup.

## What's inside

```
forgejo-mirror-kit/
├── docker-compose.yml        # Forgejo + PostgreSQL, every line commented
├── .env.example              # 3 variables to edit, no secrets committed
├── forgejo/
│   └── app.ini               # Mirror interval 8h, unnecessary features disabled
├── LICENSE                   # MIT
└── README.md                 # You are here
```

## Prerequisites

- Docker + Docker Compose (v2)
- That's it

## Setup (3 steps)

```bash
git clone https://github.com/rentierdigital/forgejo-mirror-kit.git
cd forgejo-mirror-kit
cp .env.example .env          # edit FORGEJO_DOMAIN and POSTGRES_PASSWORD
docker compose up -d
```

Open `http://localhost:3000` in your browser. Create an admin account on first visit.

## Adding a mirror

1. Log in to your Forgejo instance
2. Click **+** > **New Migration**
3. Paste your GitHub repo URL (e.g. `https://github.com/you/your-repo.git`)
4. Check **This repository will be a mirror**
5. Done - Forgejo pulls every 8 hours (configurable in `.env`)

## Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `FORGEJO_DOMAIN` | `localhost` | Domain for the Forgejo instance |
| `FORGEJO_SSH_PORT` | `2222` | SSH port mapped to host |
| `POSTGRES_PASSWORD` | - | Database password (generate a strong one) |
| `MIRROR_INTERVAL` | `8` | Hours between upstream pulls (min: 1) |

## Optional: Remote access with NetBird

Want to access your mirror from anywhere without exposing ports to the internet?

[NetBird](https://netbird.io) creates a WireGuard mesh network between your machines. Install it on the mirror host and your laptop, and you can reach Forgejo via its NetBird IP - no port forwarding, no public DNS.

## Stopping / Removing

```bash
docker compose down            # stop containers, keep data
docker compose down -v         # stop containers AND delete all data
```

---

*Built by [Rentier Digital](https://rentierdigital.xyz) - AI agents in production, not in demos.*
