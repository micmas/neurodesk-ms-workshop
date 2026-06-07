# Workshop notebook

The whole workshop is one self-contained notebook:

**[`ms_workshop.ipynb`](./ms_workshop.ipynb)**

It runs end-to-end inside Neurodesk and covers:

| Section | What it does | Tools |
|---|---|---|
| 1. Set up | Load tools into the kernel, check the Python stack | `lmod`, FSL, FreeSurfer |
| 2. Get data | Download an open MS dataset (co-registered T1/T2/FLAIR + expert lesion masks, plus a longitudinal subject) | `git` / `open_ms_data` |
| 3. Look at the data | MS lesion appearance on FLAIR vs T1 | nilearn |
| 4. Lesion segmentation | Segment WM lesions and score against the expert mask (Dice) | FreeSurfer SAMSEG |
| 5. Brain atrophy | Longitudinal percentage brain volume change (PBVC) | FSL SIENA |
| 6. Going further | Spinal cord CSA and MTR on your own data (guarded cells) | SCT, nibabel |

## How to use it

1. Start Neurodesk — easiest is [Neurodesk Play](https://play.neurodesk.org/) (browser, no install). See [`../setup/`](../setup).
2. Inside Neurodesk, open a terminal and clone this repo into persistent storage:
   ```bash
   cd /neurodesktop-storage
   git clone https://github.com/micmas/neurodesk-ms-workshop.git
   ```
3. Open `neurodesk-ms-workshop/workflows/ms_workshop.ipynb` in JupyterLab.
4. Run the cells top to bottom.

## Notes

- The dataset download (section 2) is a few hundred MB and pulls automatically — no manual setup needed.
- SAMSEG (section 4) takes ~10–20 min; everything else is quick.
- Module loading uses the Neurodesk pattern `import lmod; await lmod.load('fsl')`. If a load reports an unknown version, run `await lmod.avail('fsl')` and pin one.
- Sections 4–5 run on the downloaded open data. Section 6 (cord / qMRI) only runs if you supply your own data at the paths shown.
