# FAQ & Troubleshooting

## General

**Q: I'm new to containers — what do I need to know?**
For this workshop, nothing. Use Neurodesk Play (browser only) or run one Docker command from `setup/`. You don't need to write a Dockerfile.

**Q: Can I use my hospital scanner data?**
Yes, but ensure the data is de-identified before analysis. See `data/README.md` for a defacing example.

**Q: Do I need a GPU?**
No. The notebook runs on CPU (LST-AI is just slower without one). A GPU only helps if you go further with other deep-learning tools.

## Running the notebook

**Q: It says "module not found" for `nibabel`/`nilearn`.**
The setup cell installs these automatically. To do it by hand from a Neurodesk terminal: `pip install nibabel nilearn`.

**Q: SAMSEG runs forever.**
SAMSEG is single-threaded by default. Add `--threads 4` (or more) and it should finish in ~15 min on typical clinical 1mm T1+FLAIR.

**Q: SIENA outputs PBVC=0 or NaN.**
Usually means the brain extractions of TP1/TP2 disagree wildly. Inspect `report.html` from SIENA — it shows the registration intermediate steps.

## MS-specific

**Q: SAMSEG or LST-AI — which should I use?**
The workshop runs both side by side so you can compare:
1. **SAMSEG** — a generative atlas model, no MS training, robust across protocols and sequence-flexible.
2. **LST-AI** — a deep-learning ensemble trained on MS data; often higher Dice in-domain, and it also labels lesions by region.

Other deep-learning tools can do better in-domain but are more fragile out-of-domain — always check the training distribution against your data.

**Q: My scans are 3T but the pipeline was developed at 1.5T — does it matter?**
For SAMSEG and SIENA, no. For some deep-learning tools, yes — check the training distribution.

**Q: How do I report lesion counts vs lesion volume?**
Lesion *volume* is more reproducible. Lesion *count* requires a connected-component step (e.g. `cluster --in=lesions.nii.gz --thresh=0.5`) and is sensitive to confluent lesions.

## Reproducibility

**Q: How do I make my pipeline reproducible?**
Pin the Neurodesk image tag (e.g. `vnmd/neurodesktop:2025-04-01` instead of `latest`) and commit your notebooks + the exact `ml load <toolname>/<version>` calls.

**Q: Can I share a sealed container with my analysis?**
Yes — see Neurodesk's "build your own" docs for creating a custom container that bundles the workshop's tools at fixed versions.
