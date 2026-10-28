# Contributing to the training notebooks

Choose one notebook and one reproducible improvement. Open an issue before a major architecture or dataset change.

For a notebook change:

1. Work on a branch and use a separate environment.
2. Record Python, PyTorch, torchvision, accelerator, seed, and training settings.
3. Restart the kernel and run the affected cells in order. A saved output from an earlier run is not validation of changed code.
4. Check forward/noising shapes, one optimization step, save/load behavior, and a short sampling run before a long experiment.
5. State which cells were executed, runtime, data source, results, and remaining limits in the pull request.

For diffusion evaluation, distinguish training loss from validation metrics and sample quality. Compare configurations on the same data and sampling budget; report failed runs as well as successful ones.

Do not commit downloaded datasets, checkpoints, credentials, or large new notebook outputs. Use small annotated examples and link externally stored artifacts only when their reuse terms permit it.

No standalone LICENSE file is included. Identify third-party sources and dataset terms in any proposed addition.
