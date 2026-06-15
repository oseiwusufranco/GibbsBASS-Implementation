# GibbsBASS Reproducibility Package

This package contains the clean supplementary implementation for the manuscript:

**Gibbs Posterior-Guided Bayesian Active Sparse Sampling for Uncertainty-Aware Compressive Speech Reconstruction**

The package is designed to match the manuscript methodology and results structure. It includes a clean notebook, a reusable Python module, dependency file, and instructions for reproducing the main benchmark, ablation study, uncertainty diagnostics, and optional perceptual evaluation.

## Package contents

| File | Purpose |
|---|---|
| `GibbsBASS_Clean_Reproducibility_Notebook.ipynb` | Clean, manuscript-aligned notebook for running the complete GibbsBASS pipeline. |
| `gibbsbass_reproducibility.py` | Reusable Python implementation of GibbsBASS, baselines, ablations, metrics, diagnostics, plots, and exports. |
| `requirements.txt` | Core Python dependencies. Optional perceptual-metric packages are listed separately. |
| `README.md` | Reproducibility instructions, dataset links, and run notes. |

## Public datasets

The manuscript uses two publicly available speech datasets:

1. **LibriSpeech ASR corpus**  
   Access link: https://www.openslr.org/12/  
   Use a clean subset such as `dev-clean`, `test-clean`, or another extracted clean LibriSpeech subset as appropriate for the manuscript run.

2. **Google Speech Commands v0.02**  
   TensorFlow Datasets page: https://www.tensorflow.org/datasets/catalog/speech_commands  
   Original archive: https://storage.googleapis.com/download.tensorflow.org/data/speech_commands_v0.02.tar.gz

The notebook expects extracted dataset directories. Speech Commands v0.02 can also be downloaded automatically from the notebook or by running the Python module with `--download_speech_commands`.

## Manuscript-aligned configuration

The default full configuration follows the manuscript:

- Sampling frequency: 16,000 Hz
- Segment length: 1,024 samples
- Evaluated segments: 40
- Measurement ratios: 0.20, 0.30, 0.40
- Random seeds: 42, 123, 202
- Pilot fraction: 0.35
- Candidate blocks: 16
- Active coefficient-set size: 64
- Gibbs chains: 2
- Gibbs iterations per chain: 250
- Burn-in: 60
- Thinning: 2
- Sparsifying dictionary: orthonormal DCT
- Main method families: deterministic pursuit, structured sensing, FISTA, Bayesian sparse recovery, interpolation-guided sampling, and GibbsBASS
- Ablation variants: full GibbsBASS, no active sampling, no posterior-guided allocation, energy-only allocation, and FISTA final recovery

## How to run the notebook

1. Install dependencies:

```bash
pip install -r requirements.txt
```

For optional PESQ/STOI/ESTOI evaluation, also install:

```bash
pip install pesq pystoi
```

2. Open `GibbsBASS_Clean_Reproducibility_Notebook.ipynb`.

3. Set the dataset paths in the dataset cell:

```python
LIBRISPEECH_DIR = "/path/to/LibriSpeech/dev-clean"
SPEECH_COMMANDS_DIR = "/path/to/speech_commands_v0.02"
```

4. For a quick environment check, keep:

```python
SMOKE_TEST_MODE = True
```

This runs a small synthetic validation and does **not** reproduce the manuscript numerical tables.

5. For the full manuscript-aligned run, set:

```python
SMOKE_TEST_MODE = False
```

Then run all cells. Outputs will be written to `gibbsbass_outputs/`.

## How to run from the command line

Quick smoke test:

```bash
python gibbsbass_reproducibility.py --smoke_test --output_dir gibbsbass_smoke_outputs
```

Full run with local datasets:

```bash
python gibbsbass_reproducibility.py \
  --librispeech_dir /path/to/LibriSpeech/dev-clean \
  --speech_commands_dir /path/to/speech_commands_v0.02 \
  --output_dir gibbsbass_outputs
```

Full run with automatic Speech Commands download:

```bash
python gibbsbass_reproducibility.py \
  --librispeech_dir /path/to/LibriSpeech/dev-clean \
  --download_speech_commands \
  --output_dir gibbsbass_outputs
```

## Main outputs

The exported output directory contains:

- `main_benchmark_results.csv`
- `method_summary_ranked.csv`
- `ablation_results.csv` when full ablation is run
- `ablation_statistics.csv` when full ablation is run
- `long_form_perceptual_metrics.csv` if optional perceptual evaluation is enabled
- `gibbsbass_config.json`
- `figures/` containing ranking and selected metric plots

## Notes on reproducibility

The notebook includes a manuscript consistency audit table containing the published/manuscript reference values. Exact numerical reproduction requires the same dataset subset, segment selection, preprocessing, seeds, dependency versions, and compute environment used in the manuscript experiments. Small numerical variation may occur across BLAS/LAPACK backends, hardware, package versions, and optional perceptual-metric implementations.

## Data availability statement

The datasets used in the manuscript are publicly available. LibriSpeech is available through OpenSLR at https://www.openslr.org/12/. Google Speech Commands v0.02 is available through TensorFlow Datasets at https://www.tensorflow.org/datasets/catalog/speech_commands and through the original archive at https://storage.googleapis.com/download.tensorflow.org/data/speech_commands_v0.02.tar.gz. Processed subsets, experimental outputs, and implementation-related materials generated during the study can be regenerated using this package and may also be made available from the author upon reasonable request.
