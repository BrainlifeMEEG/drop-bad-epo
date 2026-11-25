<h1 align="center">Drop bad epochs</h1>

<p align="center">
  Drops bad epochs by index from MNE-Python epoched MEG/EEG data with Epochs.drop, taking indices from a parameter and/or a file, with before/after plots and an HTML report.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.798"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.798-blue.svg" alt="Run on brainlife.io"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-see_LICENSE-lightgrey.svg" alt="License"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Drops bad epochs by index from MNE-Python epoched MEG/EEG data with Epochs.drop, taking indices from a parameter and/or a file, with before/after plots and an HTML report.**

Reads epochs, collects the indices to remove from the drop parameter and from an optional file containing comma-separated indices (passed through the events field), removes them with mne.Epochs.drop and saves the remaining epochs together with a summary and figures. Use it to remove epochs flagged as bad by visual inspection or another QC step. Indices refer to the current epochs in the file (0-based).

| | |
|---|---|
| **Inputs** | `neuro/meeg/mne/epochs` · `neuro/meg/fif-override` (optional) |
| **Outputs** | `neuro/meeg/mne/epochs` |
| **Container** | `brainlifemeeg/mne:1.12.1` |
| **Resources** | 16 GB memory · 2.25 h walltime |
| **Run it** | [doi.org/10.25663/brainlife.app.798](https://doi.org/10.25663/brainlife.app.798) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `epo` | `neuro/meeg/mne/epochs` | yes | Epoched file to remove epochs from. |
| `events` | `neuro/meg/fif-override` | no | SPECIAL HACK: events.tsv contains a list of bad trials as a single line with comma-separated indices to drop |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `out_dir` | `neuro/meeg/mne/epochs` | MNE epochs after dropping |

<details>
<summary><b>Parameters</b> (1)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `drop` | string |  | Set epochs to remove by specifying indices to remove. Events are correspondingly modified. |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.798](https://doi.org/10.25663/brainlife.app.798), choose `neuro/meeg/mne/epochs`, `neuro/meg/fif-override` from your project, set the parameters and press **Execute**. The results are saved to your project as `neuro/meeg/mne/epochs`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlifemeeg/mne:1.12.1`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "mne": "/path/to/epo/mne",
       "events": "/path/to/events/events",
       "drop": ""
   }
   ```

3. Run `./main`.

## Configuration Parameters

| key | type | default | description |
|-----|------|---------|-------------|
| `mne` | input (`neuro/meeg/mne/epochs`) | required | path to the input MNE epochs file (`.fif` format) |
| `events` | input (`neuro/meg/fif-override`) | `""` (optional) | path to an `events.tsv`-style file whose contents are a comma-separated list of epoch indices to drop |
| `drop` | string | `""` (optional) | comma-separated list of epoch indices to drop (e.g., `"1, 5, 16"`) |

If both `events` and `drop` are provided, the union of both sets of indices is used.

## Local Testing

```bash
# Set up a config.json, e.g.:
# {
#     "mne": "in_dir/meg-epo.fif",
#     "drop": "1,5,10"
# }

./main
```

## Technical Details

- **Execution**: Python with MNE-Python and the shared `brainlife_utils` library
- **Data format**: MNE `.fif` format (compatible with all downstream Brainlife.io apps)
- **Epoch dropping**: Uses MNE's `Epochs.drop()` method for reliable epoch removal
- **Index handling**: Supports comma-separated indices or file-based index lists

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- Drop bad epochs. brainlife.io App. [doi:10.25663/brainlife.app.798](https://doi.org/10.25663/brainlife.app.798)
- Gramfort A. et al. MEG and EEG data analysis with MNE-Python. Frontiers in Neuroscience 7:267 (2013). [doi:10.3389/fnins.2013.00267](https://doi.org/10.3389/fnins.2013.00267)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- [Maximilien Chaumon](https://github.com/dnacombo), Paris Brain Institute

## Funding

[![Wellcome-226486/Z/22/Z](https://img.shields.io/badge/Wellcome-226486%2FZ%2F22%2FZ-purple.svg)](https://wellcome.org/)
[![NIH-NINDS-U24NS140384](https://img.shields.io/badge/NIH_NINDS-U24NS140384-green.svg)](https://reporter.nih.gov/project-details/11261037)
[![NIH-NINDS-UM1NS132207](https://img.shields.io/badge/NIH_NINDS-UM1NS132207-green.svg)](https://reporter.nih.gov/project-details/11411328)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://reporter.nih.gov/project-details/10262925)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://reporter.nih.gov/project-details/10428625)
[![NIH-NIMH-R01MH126699](https://img.shields.io/badge/NIH_NIMH-R01MH126699-green.svg)](https://reporter.nih.gov/project-details/10460628)
[![NIH-NIDCD-R01DC020088](https://img.shields.io/badge/NIH_NIDCD-R01DC020088-green.svg)](https://reporter.nih.gov/project-details/11140284)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-2203524](https://img.shields.io/badge/NSF_BCS-2203524-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2203524)
[![NSF-IIS-1636893](https://img.shields.io/badge/NSF_IIS-1636893-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-OAC-2148729](https://img.shields.io/badge/NSF_OAC-2148729-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148729)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-IIS-2148700](https://img.shields.io/badge/NSF_IIS-2148700-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148700)
[![NSF-OAC-1916518](https://img.shields.io/badge/NSF_OAC-1916518-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1916518)

<sub>brainlife.io, which runs this App, is publicly funded by Wellcome, the U.S. National Institutes of Health and the U.S. National Science Foundation; acknowledging that support helps keep it running.</sub>

## License

See [LICENSE](LICENSE).
