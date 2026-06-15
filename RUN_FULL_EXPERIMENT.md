# Full manuscript reproduction checklist

Before running the full experiment:

1. Download and extract LibriSpeech from https://www.openslr.org/12/.
2. Download and extract Speech Commands v0.02 from https://storage.googleapis.com/download.tensorflow.org/data/speech_commands_v0.02.tar.gz, or let the notebook/module download it.
3. Set `SMOKE_TEST_MODE=False` in the notebook.
4. Confirm the configuration matches the manuscript values in the configuration cell.
5. Run all cells and export outputs to `gibbsbass_outputs/`.
6. Compare the generated ranked summaries with the manuscript reference audit values in the final notebook cell.

The default notebook is set to smoke-test mode so reviewers can quickly validate the implementation without downloading full datasets.
