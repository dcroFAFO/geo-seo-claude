# Development findings

- The preview entry point is `scripts/webapp/app.py` (Flask CRM), not the GEO audit CLI. See `docs/base44-setup.md` for its limitations and startup checks.
- CRM data is a JSON file under `Path.home() / '.geo-prospects'`, not a database. Compose persists that directory in a named volume; do not remove it to refresh dependencies.
- A fresh checkout intentionally displays the existing empty prospect state. The UI cannot create prospects; CLI skill workflows manage them.
- Use Flask's CLI to bind externally and enable reload; executing `app.py` directly binds localhost on port 5050. Keep the interactive debugger disabled in the public preview.
- The existing CRM has no authentication; do not seed private client data for verification.
