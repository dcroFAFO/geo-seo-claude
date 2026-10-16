# Base44 development preview

## Start

```sh
docker compose -f docker-compose.base44.yml up -d
```

The existing Flask CRM at `scripts/webapp/app.py` is available on host port
3000. The repository is primarily a CLI skill collection; the preview exposes
its existing CRM, not a web version of the full audit orchestrator.

The service uses Python 3.12, installs the current `requirements.txt` at startup
into a named virtual-environment volume, and runs Flask against bind-mounted
source with automatic reload. The repository has no Python dependency lockfile.
The interactive Flask debugger is disabled. No shared application configuration
or sandbox-only code overrides are required.

## Data and credentials

No database server or external credentials are required by the CRM. It reads
`/root/.geo-prospects/prospects.json` inside the container, stored in the
`prospect_data` Docker volume alongside proposals and audits. A fresh environment
shows the application's existing empty state. No fabricated prospects are seeded.
The UI has no create-prospect form; the project's CLI skills populate that file.

The full AI audit workflow requires the separately authenticated Claude Code CLI,
as described in the repository README; that workflow is not run by Flask. Optional
browser-based CLI checks may also require Playwright browser installation.
The dashboard loads Bootstrap and HTMX from public CDNs.

## Checks

```sh
docker compose -f docker-compose.base44.yml ps
curl -f http://localhost:3000/
docker compose -f docker-compose.base44.yml logs --tail=50 web
```

The Compose healthcheck requests and validates the existing dashboard. Template
and Python edits are read from the checkout, without rebuilding an application
image. Restart the service after changing requirements to sync dependencies.

The CRM has no authentication. This configuration is for development only;
do not load sensitive client data into a publicly reachable preview.
