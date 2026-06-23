# Workshop notebooks

Three notebooks, all self-contained and run inside Neurodesk:

| Notebook | Use it for |
|---|---|
| **[`ms_workshop-clear.ipynb`](./ms_workshop-clear.ipynb)** | **Start here** — run it yourself, top to bottom (no saved outputs). |
| [`ms_workshop.ipynb`](./ms_workshop.ipynb) | The same notebook already executed — a reference with the expected outputs. |
| [`ms_workshop_benchmark.ipynb`](./ms_workshop_benchmark.ipynb) | Compares SAMSEG vs LST-AI across **all** processed subjects (Dice, detection by lesion size, clinical scores). Reads existing results — no processing. |

## What `ms_workshop-clear.ipynb` covers

| Section | What it does | Tools |
|---|---|---|
| 1. Set up | Load the tools, install the Python stack, set the working directory | `module`, FSL, FreeSurfer, LST-AI |
| 2. Get data | Download an open MS dataset (co-registered T1/T2/FLAIR + expert lesion masks, plus a longitudinal subject) | `git` |
| 3. Look at the data | Interactive views of MS lesions on FLAIR vs T1 | NiiVue |
| 4. Lesion segmentation | Segment WM lesions with SAMSEG and LST-AI, score against the expert mask (Dice) | FreeSurfer SAMSEG, LST-AI |
| 5. Brain atrophy | Longitudinal percentage brain volume change (PBVC) | FSL SIENA |
| 6. Group analysis | Repeat across several subjects; relate lesion load to disability (EDSS) | nibabel, nilearn, pandas |

## How to use it

1. Start Neurodesk — easiest is [Neurodesk Play](https://play.neurodesk.org/) (browser, no install). See [`../setup/`](../setup).
2. In a Neurodesk terminal, clone this repo into persistent storage:
   ```bash
   cd /neurodesktop-storage
   git clone https://github.com/micmas/neurodesk-ms-workshop.git
   ```
3. Open `neurodesk-ms-workshop/workflows/ms_workshop-clear.ipynb` in JupyterLab.
4. Run the cells top to bottom.

## Good to know

- **Working directory** — the *Configuration* cell sets `WORK`. Leave the default to download data and write results under your own storage, or point it at a folder of pre-computed results to skip the slow steps.
- **Caching** — each analysis step checks for its output first and skips if it already exists (delete the step's folder to force a re-run).
- **Timing** — every step is timed; a summary table is printed at the end.
- **Runtimes** — SAMSEG is ~10–20 min and LST-AI ~15–40 min on a CPU; SIENA and the rest are quick. The dataset download (section 2) is a few hundred MB and runs automatically.
- **Choosing a subject** — the *Configuration* cell has a `SUBJECT` option; leave it `None` to auto-select a complete subject, or pin one (e.g. `'patient07'`).
