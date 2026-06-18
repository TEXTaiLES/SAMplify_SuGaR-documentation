
# Installation

NEPHELE is split into two components on separate branches:

| Branch | What it does |
|--------|-------------|
| `nefele-training` | **Backend** — runs SAM2, COLMAP, and SuGaR/PGSR inside Docker containers |
| `nefele_ui` | **Web UI** — browser-based interface for uploading images, annotating, and downloading results |

You can use the **backend alone** (scriptable, no browser needed) or combine both for a full web experience.

---

## Requirements

Make sure the following are installed on the machine that will run the pipeline:

- **Docker** with the Compose plugin v2 (`docker compose`, not `docker-compose`)
- **NVIDIA GPU** with up-to-date drivers
- **NVIDIA Container Toolkit** — needed so Docker containers can access the GPU
- **Python 3** with the `requests` library — needed for the host-side worker poller

Verify that your GPU is accessible inside Docker before continuing:

```bash
docker run --rm --gpus all nvidia/cuda:12.1-base nvidia-smi
```

You should see your GPU listed. If not, check your NVIDIA Container Toolkit installation.

---

## 1. Clone the Backend (`nefele-training`)

```bash
git clone --recurse-submodules -b nefele-training \
    https://github.com/TEXTaiLES/SAMplify_SuGaR.git
cd SAMplify_SuGaR
```

If you forgot `--recurse-submodules`, run this afterwards to pull the submodules:

```bash
git submodule update --init --recursive
```

---

## 2. Clone the UI (`nefele_ui`) — optional

The UI lives on a separate branch. Clone it into a sibling folder:

```bash
git clone -b nefele_ui \
    https://github.com/TEXTaiLES/SAMplify_SuGaR.git SAMplify_SuGaR_ui
cd SAMplify_SuGaR_ui/nefele_ui
```

---

## 3. Configure Environment Variables

Both components are configured via a `.env` file copied from the provided example.

### Backend

From inside the `SAMplify_SuGaR` folder:

```bash
cp .env.example .env
```

Open `.env` and fill in the following:

| Variable | Description |
|----------|-------------|
| `HOST_UID` | Your Linux user ID — run `id -u` to get it |
| `HOST_GID` | Your Linux group ID — run `id -g` to get it |
| `HESTIA_API_KEY` | API key for the HESTIA job queue — leave blank for standalone use |
| `HESTIA_API_URL` | HESTIA API endpoint (default: `https://api.textailes.athenarc.gr`) |
| `IN_MNT` | Absolute path on the host where input images will be read from |
| `OUT` | Absolute path on the host where outputs will be written |
| `WEB_PORT` | Port for the SAM2 web interface (default: `8092`) |

### UI

From inside the `SAMplify_SuGaR_ui/nefele_ui` folder:

```bash
cp .env.example .env
```

Key variables to set:

| Variable | Description |
|----------|-------------|
| `SAMPLIFY_ROOT` | Absolute path to your cloned `nefele-training` directory |
| `COMMS_BACKEND` | `shared_fs` for local deployments (default), `vm_comms` for remote |
| `HESTIA_API_KEY` | API key for HESTIA integration (optional for local use) |
| `WEB_PORT` | Port to expose the UI on (default: `8092`) |

---

## 4. Build the Docker Images

### Backend

From inside the `SAMplify_SuGaR` folder:

```bash
docker compose build
```

The PGSR container clones additional repositories during its first build — this can take several minutes depending on your internet connection.

### UI

From inside the `SAMplify_SuGaR_ui/nefele_ui` folder:

```bash
docker compose build
```

---

## Next Step

Once the images are built, continue to:

**[Dataset Preparation →](dataset_preparation.md)**
