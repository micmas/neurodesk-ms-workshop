# Example datasets for the workshop

We do **not** ship datasets in this repo (size + licensing). Instead, here are pointers to openly-available MS imaging datasets you can download into Neurodesk and use with the workflow notebooks.

## Recommended for the workshop

### MSSEG-1 / MSSEG-2 challenges
Multi-site MS lesion segmentation challenges with FLAIR + T1 + T2.

- **MSSEG-2 (2021)** — https://portal.fli-iam.irisa.fr/msseg-2/
- Registration required. 100 patients, two timepoints each — perfect for the longitudinal demo (notebook 03).

### OpenNeuro datasets

OpenNeuro hosts many open MS datasets in BIDS format. Filter by "multiple sclerosis" at https://openneuro.org/.

Notable examples:
- **ds004078** — Longitudinal MS imaging
- **ds002080** — White matter lesions in MS
- **ds003505** — 7T qMRI in MS

### Neurodesk's bundled examples
Neurodesk Play already includes small example datasets in `/data/` — quickest path for the validation notebook (00).

## How to download

Inside Neurodesk, in a terminal:

```bash
cd /neurodesktop-storage
mkdir ms-workshop-data && cd ms-workshop-data

# Example: OpenNeuro dataset via DataLad
ml load datalad
datalad clone https://github.com/OpenNeuroDatasets/ds004078.git
cd ds004078
datalad get sub-001/   # only fetch one subject to save space
```

Or with `aws s3` (no account needed for OpenNeuro):
```bash
aws s3 sync --no-sign-request s3://openneuro.org/ds004078/sub-001 ./sub-001
```

## Expected layout for the notebooks

The notebooks assume a BIDS-ish layout under `/neurodesktop-storage/ms-workshop-data/`:

```
ms-workshop-data/
├── sub-001/
│   ├── anat/
│   │   ├── sub-001_T1w.nii.gz
│   │   └── sub-001_FLAIR.nii.gz
│   └── cord/
│       └── sub-001_T2w_cord.nii.gz
└── sub-001-longitudinal/
    ├── sub-001_ses-01_T1w.nii.gz
    └── sub-001_ses-02_T1w.nii.gz
```

Adjust paths at the top of each notebook to match your data.

## Ethics & consent reminder

If using **patient data** (not public datasets), make sure:
- Data is fully de-identified (DICOM headers stripped, faces defaced — try `pydeface` or `mri_deface` from FreeSurfer)
- Local IRB / ethics approval covers analysis with cloud or container tools
- Data is **not** committed to this repo. The `.gitignore` already excludes `/data/raw/` and `*.nii.gz`.

## Defacing example

```bash
ml load freesurfer
mri_deface input_T1.nii.gz \
  $FREESURFER_HOME/average/talairach_mixed_with_skull.gca \
  $FREESURFER_HOME/average/face.gca \
  defaced_T1.nii.gz
```
