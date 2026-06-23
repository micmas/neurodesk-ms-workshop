# Setting up Neurodesk

This workshop runs inside **Neurodesk**. For the workshop, the easiest option is **Neurodesk Play** — it runs in your browser, nothing to install.

## Recommended: Neurodesk Play

1. Go to **https://play.neurodesk.org/** and sign in (a GitHub account works).
2. Launch a session — you get a full Linux desktop with the neuroimaging tools preinstalled.
3. Open a terminal and clone this repo:
   ```bash
   cd /neurodesktop-storage
   git clone https://github.com/micmas/neurodesk-ms-workshop.git
   ```

Play sessions are time-limited with limited storage — fine for the workshop. For heavy or offline work, install Neurodesk locally (below).

## Other ways to run Neurodesk

Neurodesk also runs on your own laptop (Docker), on HPC, and in the cloud. Instead of duplicating instructions that go out of date, use the official, always-current guide and pick your platform:

**→ https://neurodesk.org/getting-started/**

- Browser / cloud (Play, Colab, Codespaces): https://neurodesk.org/getting-started/hosted/
- Local install (Neurodesktop — Linux / Mac / Windows): https://neurodesk.org/getting-started/neurodesktop/
- Command line / HPC (Neurocommand): https://neurodesk.org/getting-started/neurocommand/

## Check it works

In a Neurodesk terminal:

```bash
ml load fsl && flirt -version
ml load freesurfer && mri_convert --version
```

If each prints a version, you're set. Section 1 of the workshop notebook ([`workflows/ms_workshop-clear.ipynb`](../workflows/ms_workshop-clear.ipynb)) runs the same check from inside Neurodesk.

Stuck? See the getting-started guide above, or ask on the Neurodesk discussions board: https://github.com/orgs/neurodesk/discussions
