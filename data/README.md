# Data

No imaging data is stored in this repo (size + licensing). The notebook downloads what it needs automatically.

## What the workshop uses

The notebook clones the **[open_ms_data](https://github.com/muschellij2/open_ms_data)** repository (a few hundred MB, fetched automatically in section 2). It packages the **Ljubljana 3D MS lesion benchmark**: co-registered, N4-corrected T1 / T2 / FLAIR with **expert consensus lesion masks**, plus a small longitudinal set. It also ships per-patient clinical data (age, sex, MS type, EDSS) used in the group analysis.

> Lesjak Ž, et al. *A Novel Public MS Lesion Segmentation Benchmark.* Neuroinformatics 16, 51–63 (2018).

You don't need to download anything by hand — just run the notebook.

## Other open MS datasets

If you want to try the workflow on more data:

- **OpenNeuro** — filter by "multiple sclerosis" at https://openneuro.org/ (e.g. `ds004078` longitudinal MS, `ds002080` white-matter lesions, `ds003505` 7T qMRI). Fetch with DataLad inside Neurodesk:
  ```bash
  ml load datalad
  datalad clone https://github.com/OpenNeuroDatasets/ds004078.git
  cd ds004078 && datalad get sub-001/   # one subject at a time to save space
  ```
- **MSSEG-1 / MSSEG-2** challenges — multi-site MS lesion segmentation with FLAIR + T1 + T2 (registration required): https://portal.fli-iam.irisa.fr/msseg-2/

To use your own data, point the `SUBJECT`/paths in the notebook at your T1 + FLAIR (+ an expert mask if you want a Dice score).

## Using your own patient data — ethics & de-identification

If you analyse **patient data** (not public datasets), make sure:

- Data is fully de-identified — DICOM headers stripped and faces defaced (`pydeface`, or `mri_deface` from FreeSurfer).
- Local IRB / ethics approval covers analysis in a container or cloud environment.
- Data is **not** committed to this repo — `.gitignore` already excludes `*.nii.gz`, `*.dcm`, and the output folders.

Defacing example:

```bash
ml load freesurfer
mri_deface input_T1.nii.gz \
  $FREESURFER_HOME/average/talairach_mixed_with_skull.gca \
  $FREESURFER_HOME/average/face.gca \
  defaced_T1.nii.gz
```
