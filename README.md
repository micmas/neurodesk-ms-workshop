# Neurodesk for Multiple Sclerosis: A Clinical Workshop

A hands-on workshop introducing **Neurodesk** — a containerised, reproducible neuroimaging analysis environment — with a focus on **clinical applications in Multiple Sclerosis (MS)**.

This repository contains all workshop materials: slides, example workflows, dataset pointers, and setup instructions.

---

## What is Neurodesk?

[Neurodesk](https://www.neurodesk.org/) is a free, open-source platform that bundles 90+ neuroimaging tools (FSL, FreeSurfer, ANTs, MRtrix3, AFNI, SPM, and more) into a portable container environment. It runs anywhere — laptops, HPC clusters, or in the browser via Neurodesk Play — and lets researchers and clinicians run reproducible analyses without manually installing each package.

## Why MS?

Multiple Sclerosis presents specific imaging challenges that benefit directly from reproducible pipelines:

- **Lesion detection and segmentation** on T2-FLAIR / T1-weighted sequences
- **Longitudinal change** tracking (lesion load, brain volume, atrophy)
- **Quantitative MRI** (T1/T2 mapping, MTR, susceptibility) for tissue characterisation
- **Spinal cord imaging** — often as important as brain imaging in MS
- **Cross-site harmonisation** for multi-centre clinical studies and trials

## Workshop Structure

| Section | Folder | Description |
|---|---|---|
| Slides | [`slides/`](./slides) | Presentation deck (PPTX/PDF) |
| Setup guide | [`setup/`](./setup) | Install Neurodesk on your machine |
| Example workflows | [`workflows/`](./workflows) | Jupyter notebooks for MS imaging tasks |
| Dataset pointers | [`data/`](./data) | Where to find example MS datasets |
| Extras | [`docs/`](./docs) | Reference materials, FAQ, troubleshooting |

## Quick Start

1. **Install Neurodesk** — see [`setup/README.md`](./setup/README.md). Easiest option: open [Neurodesk Play](https://play.neurodesk.org/) in your browser, no install needed.
2. **Get example data** — see [`data/README.md`](./data/README.md). We use openly available MS datasets.
3. **Run a workflow** — open the notebooks in [`workflows/`](./workflows) inside Neurodesk and follow along.

## Audience

Clinicians, radiologists, neurologists, MS researchers, and imaging scientists. No prior containerisation or scripting experience required, though Python/shell familiarity helps for the workflow sections.

## License

Materials are released under [CC BY 4.0](./LICENSE) — feel free to reuse and adapt with attribution.

## Citation

If these materials help your work, please cite Neurodesk:

> Renton, A.I., Dao, T.T., Johnstone, T. et al. *Neurodesk: an accessible, flexible and portable data analysis environment for reproducible neuroimaging.* Nature Methods 21, 804–808 (2024). https://doi.org/10.1038/s41592-023-02145-x

## Contact

Questions or issues? Open an issue on this repo or reach out to the workshop organiser.
