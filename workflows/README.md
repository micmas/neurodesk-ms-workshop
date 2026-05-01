# Example Workflows

These notebooks demonstrate typical MS imaging analyses inside Neurodesk. Each one is self-contained and uses openly available example data — see [`../data/`](../data) for download instructions.

| # | Notebook | What it covers |
|---|---|---|
| 00 | [`00_validate_setup.ipynb`](./00_validate_setup.ipynb) | Confirms Neurodesk modules load (FSL, ANTs, FreeSurfer, MRtrix3) |
| 01 | [`01_preprocessing_t1_flair.ipynb`](./01_preprocessing_t1_flair.ipynb) | Brain extraction, bias correction, T1↔FLAIR coregistration |
| 02 | [`02_lesion_segmentation_samseg.ipynb`](./02_lesion_segmentation_samseg.ipynb) | WM lesion segmentation with FreeSurfer SAMSEG |
| 03 | [`03_brain_volumetry_longitudinal.ipynb`](./03_brain_volumetry_longitudinal.ipynb) | Longitudinal brain volume change with SIENA |
| 04 | [`04_spinal_cord_toolbox.ipynb`](./04_spinal_cord_toolbox.ipynb) | Cord segmentation and CSA with Spinal Cord Toolbox |
| 05 | [`05_quantitative_mri.ipynb`](./05_quantitative_mri.ipynb) | T1/T2 mapping and MTR analysis |

## How to use these notebooks

1. Start Neurodesk (see [`../setup/`](../setup))
2. Inside Neurodesk, open a terminal and clone this repo:
   ```bash
   cd /neurodesktop-storage
   git clone https://github.com/<your-username>/neurodesk-ms-workshop.git
   cd neurodesk-ms-workshop/workflows
   ```
3. Launch JupyterLab from the Neurodesk menu and open the notebook of interest
4. Run cells top to bottom

## Module loading pattern

Inside any notebook, neuroimaging tools are loaded with `ml`:

```python
import subprocess
def ml(cmd):
    subprocess.run(f"bash -lc 'ml load {cmd}'", shell=True, check=True)

ml("fsl")
ml("freesurfer")
ml("mrtrix3")
```

Or from a terminal cell:
```bash
%%bash
ml load fsl
bet input.nii.gz output_brain.nii.gz -f 0.4
```

## Notes for the workshop

- **00** and **01** are the warm-up — everyone should run these.
- **02** is the core MS demo (lesion segmentation).
- **03–05** are advanced; cover whichever fits the audience.

> The `.ipynb` files in this folder are starter scaffolds. Workshop attendees will add cells live during the session, then push their version back to a fork.
