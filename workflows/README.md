# Workshop notebook

The whole workshop is one self-contained notebook:

**[`ms_workshop.ipynb`](./ms_workshop.ipynb)**

It runs end to end inside Neurodesk and covers:

| Section | What it does | Tools |
|---|---|---|
| 1. Set up | Load the tools, install the Python stack, set the working directory | `module`, FSL, FreeSurfer |
| 2. Get data | Download an open MS dataset (co-registered T1/T2/FLAIR + expert lesion masks, plus a longitudinal subject) | `git` |
| 3. Look at the data | Interactive views of MS lesions on FLAIR vs T1 | NiiVue |
| 4. Lesion segmentation | Segment WM lesions with SAMSEG and LST-AI, score against the expert mask (Dice) | FreeSurfer SAMSEG, LST-AI |
| 5. Brain atrophy | Longitudinal percentage brain volume change (PBVC) | FSL SIENA |
| 6. Going further | Spinal cord CSA and MTR on your own data | SCT, nibabel |

## How to use it

1. Start Neurodesk — easiest is [Neurodesk Play](https://play.neurodesk.org/) (browser, no install). See [`../setup/`](../setup).
2. In a Neurodesk terminal, clone this repo into persistent storage:
   ```bash
   cd /neurodesktop-storage
   git clone https://github.com/micmas/neurodesk-ms-workshop.git
   ```
3. Open `neurodesk-ms-workshop/workflows/ms_workshop.ipynb` in JupyterLab.
4. Run the cells top to bottom.

## Good to know

- **Working directory** — the *Configuration* cell sets `WORK`. Leave the default to download data and write results under your own storage, or point it at a folder of pre-computed results to skip the slow steps.
- **Caching** — each analysis step checks for its output first and skips if it already exists (delete the step's folder to force a re-run).
- **Timing** — every step is timed; a summary table is printed at the end.
- **Runtimes** — SAMSEG is ~10–20 min and LST-AI ~15–40 min on a CPU; SIENA and the rest are quick. The dataset download (section 2) is a few hundred MB and runs automatically.
- **Your own data** — sections 4–5 run on the downloaded open data; section 6 (cord / qMRI) runs only if you supply your own data at the paths shown.
