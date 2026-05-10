# Pickfolio Infra

Shared deployment configuration for Pickfolio.

This repo owns the server-level files used by Docker Compose:

- `docker-compose.yml`
- `nginx.conf`
- `db-init/`
- `.env.example`

Do not commit the real `.env` file. Keep production secrets on the Oracle VM and in GitHub Actions secrets.

## Deployment

Pushes to `main` deploy the shared config to:

```text
/home/ubuntu/pickfolio
```

The workflow syncs `docker-compose.yml`, `nginx.conf`, and `db-init/`, then runs:

```bash
docker compose up -d
docker compose restart pickfolio-ui
```

Restarting `pickfolio-ui` reloads the mounted nginx config.

