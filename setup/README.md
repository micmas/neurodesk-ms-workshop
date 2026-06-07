# Setting up Neurodesk

This workshop runs entirely inside **Neurodesk**. You have three options, in order of ease:

1. **[Neurodesk Play](#option-1-neurodesk-play-zero-install)** — browser only, no install (easiest, recommended for the workshop)
2. **[Neurodesktop (Docker)](#option-2-neurodesktop-via-docker)** — full local install, persistent
3. **[Neurocommand (CLI only)](#option-3-neurocommand-cli)** — command-line tools on Linux/macOS without the desktop UI

> **TL;DR for workshop attendees:** Use Neurodesk Play unless you need to work with your own data offline. It works on any machine with a modern browser.

---

## Option 1: Neurodesk Play (zero install)

Neurodesk Play is a free hosted version that runs in your browser.

1. Go to **https://play.neurodesk.org/**
2. Sign in (GitHub account works)
3. Launch a session — you get a full Linux desktop with all neuroimaging tools preinstalled
4. Upload your data, or clone this repo from the terminal:
   ```bash
   git clone https://github.com/micmas/neurodesk-ms-workshop.git
   ```

**Limits:** Neurodesk Play is for trying things out — sessions are time-limited and storage is small. For real analyses, install locally.

---

## Option 2: Neurodesktop via Docker

Best if you have a reasonably powerful laptop (16 GB+ RAM recommended) and want a persistent, full-featured environment.

### Prerequisites

- **Docker Desktop** installed and running
  - macOS: https://docs.docker.com/desktop/install/mac-install/
  - Windows: https://docs.docker.com/desktop/install/windows-install/ (enable WSL2)
  - Linux: https://docs.docker.com/engine/install/

### Run Neurodesktop

Pick a folder on your computer to store data and notebooks (e.g. `~/neurodesktop-storage`), then run:

**macOS / Linux:**
```bash
mkdir -p ~/neurodesktop-storage
docker run \
    --shm-size=1gb -it --privileged --name neurodesktop \
    -v ~/neurodesktop-storage:/neurodesktop-storage \
    -e NB_UID="$(id -u)" -e NB_GID="$(id -g)" \
    -p 8888:8888 \
    vnmd/neurodesktop:latest
```

**Windows (PowerShell):**
```powershell
mkdir $HOME\neurodesktop-storage
docker run --shm-size=1gb -it --privileged --name neurodesktop `
    -v $HOME\neurodesktop-storage:/neurodesktop-storage `
    -p 8888:8888 `
    vnmd/neurodesktop:latest
```

Open http://localhost:8888 in your browser. You'll see a full Linux desktop.

### After first run

To start/stop the container:
```bash
docker start neurodesktop    # start existing container
docker stop neurodesktop     # stop without losing state
docker rm neurodesktop       # delete (storage folder is preserved)
```

To update to the latest image:
```bash
docker pull vnmd/neurodesktop:latest
```

---

## Option 3: Neurocommand (CLI)

If you only want command-line tools (no desktop), Neurocommand provides Lmod-style modules on Linux/macOS.

See https://www.neurodesk.org/docs/getting-started/neurocommand/ — covered briefly during the workshop.

---

## Validation: did it work?

Once Neurodesk is running, open a terminal inside it and run:

```bash
ml load fsl
flirt -version
ml load mrtrix3
mrconvert -version
ml load freesurfer
mri_convert --version
```

If each command prints a version, you're set.

You can also try the validation notebook: [`workflows/00_validate_setup.ipynb`](../workflows/00_validate_setup.ipynb).

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Docker container won't start, port 8888 in use | Change `-p 8888:8888` to `-p 8889:8888` and visit `localhost:8889` |
| "no space left on device" | Docker Desktop → Resources → increase disk image size |
| Slow performance on Mac M1/M2/M3 | Already supported (multi-arch image); ensure you're on the latest Docker Desktop |
| Tool not found inside Neurodesk | Run `ml avail` to list modules, then `ml load <toolname>` |

For more help: https://www.neurodesk.org/docs/getting-started/troubleshooting/
