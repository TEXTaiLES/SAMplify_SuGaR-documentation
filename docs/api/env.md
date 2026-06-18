# Environment Variables

Both components are configured via a `.env` file copied from `.env.example`. This page lists every variable for each branch.

---

## nefele-training (backend)

Copy the template:
```bash
cp .env.example .env
```

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `DATASET_NAME` | _(empty)_ | No | Optional identifier for the active dataset |
| `WEB_PORT` | `8092` | No | Port for the SAM2 annotation interface |
| `HOST_UID` | `1000` | Yes | Host user ID — run `id -u` to get yours |
| `HOST_GID` | `1000` | Yes | Host group ID — run `id -g` to get yours |
| `HESTIA_API_KEY` | _(empty)_ | No | API key for HESTIA job queue; leave blank for standalone use |
| `HESTIA_API_URL` | `https://api.textailes.athenarc.gr` | No | HESTIA API endpoint |
| `IN_MNT` | `/opt/samplify_sugar/SAM2/data/input` | Yes | Absolute host path for input images (used by worker_poller) |
| `OUT` | `/opt/samplify_sugar/SAM2/data/output` | Yes | Absolute host path for pipeline outputs (used by worker_poller) |

---

## nefele_ui (frontend)

From inside the `nefele_ui/` folder:
```bash
cp .env.example .env
```

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `DATASET_NAME` | _(empty)_ | No | Optional identifier for the active dataset |
| `WEB_PORT` | `8092` | No | Port to expose the UI on |
| `HOST_UID` | `1000` | Yes | Host user ID |
| `HOST_GID` | `1000` | Yes | Host group ID |
| `SAMPLIFY_ROOT` | `/home/vaia/samplify_sugar` | Yes | Absolute path to the cloned `nefele-training` directory |
| `COMMS_BACKEND` | `shared_fs` | No | Transport between UI and SAM2 worker: `shared_fs` for local, `vm_comms` for remote |
| `VM_COMMS_POLL_INTERVAL` | `2` | No | Polling interval in seconds (used when `COMMS_BACKEND=vm_comms`) |
| `WORKER_URL` | `http://sam2:5001` | No | HTTP endpoint of the SAM2 worker container |
| `WORKER_TIMEOUT` | `600` | No | Request timeout in seconds for the worker |
| `HESTIA_API_URL` | `http://api.textailes.athenarc.gr` | No | HESTIA API endpoint |
| `HESTIA_API_KEY` | _(empty)_ | No | API key for HESTIA integration |
| `AUTH_ENABLED` | `0` | No | Set to `1` to enable SSO authentication via Directus |
| `DIRECTUS_URL` | `https://textailes.athenarc.gr` | No | Directus SSO endpoint (only used if `AUTH_ENABLED=1`) |
| `APP_BASE` | `http://nephele.textailes.athenarc.gr:8093` | No | Public base URL of the app (used in auth redirects) |
| `AUTH_COOKIE_NAME` | `textailes_refresh_token` | No | Name of the SSO cookie |
| `AUTH_COOKIE_DOMAIN` | `.textailes.athenarc.gr` | No | Domain for the SSO cookie |
