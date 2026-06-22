# Neurodesk for Multiple Sclerosis — a hands-on workshop

Hands-on workshop materials for running reproducible **Multiple Sclerosis (MS)** neuroimaging analyses in **[Neurodesk](https://www.neurodesk.org/)**, a free, containerised environment that bundles 90+ neuroimaging tools (FSL, FreeSurfer, ANTs, MRtrix3, AFNI, SPM, and more) and runs on a laptop, an HPC cluster, or in the browser via [Neurodesk Play](https://play.neurodesk.org/).

## Quick start

1. **Open Neurodesk** — go to [play.neurodesk.org](https://play.neurodesk.org/) (browser, no install). Other options are in [`setup/`](./setup).
2. **Clone this repo** in a Neurodesk terminal:
   ```bash
   cd /neurodesktop-storage
   git clone https://github.com/micmas/neurodesk-ms-workshop.git
   ```
3. **Run the notebook** — open [`workflows/ms_workshop.ipynb`](./workflows/ms_workshop.ipynb) and run it top to bottom. It downloads the data and walks through the analyses.

## What the workshop covers

The notebook runs a complete MS imaging pipeline, one step at a time:

1. Load the tools and set the working directory
2. Download an open MS dataset
3. View lesions on FLAIR vs T1 (interactive)
4. White-matter lesion segmentation — FreeSurfer **SAMSEG** and **LST-AI**, scored against an expert mask (Dice)
5. Longitudinal brain atrophy — FSL **SIENA**
6. Going further — spinal cord (SCT) and quantitative MRI (MTR) on your own data

Each analysis step is **timed** and **skipped automatically** if its results already exist, so the working directory can be pointed at a folder of pre-computed results to save time.

## Repository layout

| Folder | Contents |
|---|---|
| [`workflows/`](./workflows) | The workshop notebook, `ms_workshop.ipynb` |
| [`setup/`](./setup) | How to run Neurodesk (Play, Docker, CLI) |
| [`data/`](./data) | Pointers to open MS datasets |
| [`docs/`](./docs) | FAQ and troubleshooting |
| [`slides/`](./slides) | Presentation and hands-on guide |

## Audience

Clinicians, radiologists, neurologists, MS researchers, and imaging scientists. No containerisation experience needed; basic Python/shell familiarity helps for the analysis sections.

## License

Released under [CC BY 4.0](./LICENSE) — reuse and adapt with attribution.

## Citation

> Renton, A.I., Dao, T.T., Johnstone, T. et al. *Neurodesk: an accessible, flexible and portable data analysis environment for reproducible neuroimaging.* Nature Methods 21, 804–808 (2024). https://doi.org/10.1038/s41592-023-02145-x

## Contact

Open an issue on this repository or reach out to the workshop organiser.
