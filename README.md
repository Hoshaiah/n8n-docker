# n8n Docker Setup

A Docker Compose setup for running [n8n](https://n8n.io) locally with PostgreSQL.

## Services

- **n8n** — Workflow automation platform, accessible at `http://localhost:5678`
- **PostgreSQL 16** — Database backend for n8n

## Quick Start

```bash
docker compose up -d
```

Then open [http://localhost:5678](http://localhost:5678) in your browser.

Default credentials:
- **Username:** `admin`
- **Password:** `admin`

> **Important:** Change the default passwords in `docker-compose.yml` before exposing this to any network beyond localhost.

## Configuration

Key environment variables you may want to change:

| Variable | Default | Description |
|---|---|---|
| `POSTGRES_PASSWORD` | `n8n_test_password` | PostgreSQL password |
| `N8N_BASIC_AUTH_USER` | `admin` | n8n login username |
| `N8N_BASIC_AUTH_PASSWORD` | `admin` | n8n login password |
| `GENERIC_TIMEZONE` | `UTC` | Timezone for scheduled workflows |

## Claude MCP Integration (Optional)

The compose file includes a commented-out [n8n-mcp](https://github.com/czlonkowski/n8n-mcp) service for integrating n8n with Claude. To enable it:

1. Uncomment the `n8n-mcp` service in `docker-compose.yml`
2. Generate an API key in n8n (Settings > API)
3. Set the `N8N_API_KEY` environment variable:
   ```bash
   export N8N_API_KEY="your-api-key-here"
   ```

## Data Persistence

Data is stored in Docker volumes:
- `postgres_data` — PostgreSQL database
- `n8n_data` — n8n workflows, credentials, and settings

To reset everything:
```bash
docker compose down -v
```
