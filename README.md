# Drop Bad Epochs

[![Run on Brainlife.io](https://img.shields.io/badge/Brainlife-bl.app.798-blue.svg)](https://doi.org/10.25663/brainlife.app.798)

## Description

Drops (rejects) bad epochs from MNE Epochs files by their indices using MNE-Python's [Epochs.drop()](https://mne.tools/stable/generated/mne.Epochs.html#mne.Epochs.drop) method. This app is useful for:
- Removing epochs marked as artifacts or bad quality
- Removing epochs by index from a separate quality control analysis
- Cleaning up epoched data for subsequent analysis

The app generates:
- An epochs file with the specified epochs removed
- A text summary of the dropped epochs
- An HTML report with before/after epoch visualizations
- A `product.json` with metadata about the dropped epochs

## Inputs

- **`mne`** (`neuro/meeg/mne/epochs`): epoched file to remove epochs from (required)
- **`events`** (`neuro/meg/fif-override`): special-case input whose `events.tsv` contains a single line of comma-separated indices of bad trials to drop (optional)

## Outputs

- **`out_dir/meg-epo.fif`** (`neuro/meeg/mne/epochs`): epochs file with the specified epochs removed
- **`out_dir/info.txt`**: summary of dropped and remaining epochs
- **`out_figs/`**: PNG plots of epochs before dropping and of the epochs dropped from the `events` file / `drop` config
- **`out_report/report.html`**: HTML report with the original, dropped, and remaining epochs
- **`product.json`**: metadata about dropped epochs

## Configuration Parameters

| key | type | default | description |
|-----|------|---------|-------------|
| `mne` | input (`neuro/meeg/mne/epochs`) | required | path to the input MNE epochs file (`.fif` format) |
| `events` | input (`neuro/meg/fif-override`) | `""` (optional) | path to an `events.tsv`-style file whose contents are a comma-separated list of epoch indices to drop |
| `drop` | string | `""` (optional) | comma-separated list of epoch indices to drop (e.g., `"1, 5, 16"`) |

If both `events` and `drop` are provided, the union of both sets of indices is used.

## Usage

### Running on Brainlife.io

1. Go to the [drop-bad-epo app page](https://brainlife.io/app/64f993aee4d2e9108d92bb8c) on Brainlife.io.
2. Select an MNE epochs file as the `mne` input.
3. Optionally select an `events` input, and/or set the `drop` parameter to a comma-separated list of epoch indices.
4. Submit the process and retrieve the resulting epochs file, report, and `product.json` once it completes.

### Local Testing

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

## Authors

- [Maximilien Chaumon](https://github.com/dnacombo), Paris Brain Institute

## Citations

We kindly ask that you cite the following articles when publishing papers and code using this app:

Hayashi, S., Caron, B.A., Heinsfeld, A.S. et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. Nat Methods 21, 809–813 (2024). https://doi.org/10.1038/s41592-024-02237-2

Gramfort, A. et al. MEG and EEG data analysis with MNE-Python. Front. Neurosci. 7, 267 (2013). https://doi.org/10.3389/fnins.2013.00267

## Funding Acknowledgement

brainlife.io is publicly funded and for the sustainability of the project we kindly ask that you acknowledge the following funding sources:

[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-ACI-1916518](https://img.shields.io/badge/NSF_ACI-1916518-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1916518)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://grantome.com/grant/NIH/R01-EB029272-01)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://grantome.com/grant/NIH/R01-EB030896-01)

## License

Copyright (c) 2026 MEEG Brainlife team. Licensed under AGPL-3.0, see [license.txt](license.txt).
