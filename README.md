# Generative-model training notebooks

Two exploratory notebooks for learning how generative models are trained. The diffusion notebook implements a class-conditioned image model; the dialogue notebook builds a tokenizer and language model around a movie-dialogue dataset.

These are research exercises with saved outputs, not packaged applications or validated model releases.

## Notebooks

| Notebook | Implementation | Current evidence |
| --- | --- | --- |
| [Conditional diffusion](controlled-diffusion.ipynb) | MNIST at 32×32, 1,000-step linear noise schedule, residual U-Net with timestep/class embeddings and attention, noise-prediction MSE, reverse sampling | Saved loss logs and generated examples; no held-out image-quality benchmark |
| [Dialogue generator](hp-dialog-generator.ipynb) | Dialogue preprocessing, byte-level BPE tokenizer, and a PyTorch language-model experiment | Historical notebook outputs; requires the original external CSV layout |

## Inspect or run the diffusion experiment

Open the notebook on GitHub to inspect its code and saved outputs without installing anything. Running it requires PyTorch, a matching torchvision build, NumPy, Matplotlib, and a Jupyter environment. The original environment was Kaggle; no locked environment is supplied.

For a local session:

```bash
git clone https://github.com/Kartik-A-1820/2025.git
cd 2025
python -m venv .venv
```

Activate with `source .venv/bin/activate` on Linux/macOS or `.venv\Scripts\Activate.ps1` in PowerShell. Install PyTorch and torchvision for your platform, then:

```bash
python -m pip install numpy matplotlib jupyterlab
python -m jupyter lab
```

Before executing the diffusion training cells:

1. Replace the notebook's `/kaggle/working` output paths with one writable working directory. Keep the `generated/` and `checkpoints/` save/load paths consistent. The original notebook mixes absolute and relative paths.
2. Set a short training run before attempting the original 200 epochs. MNIST downloads on first use; a compatible GPU is recommended for the full experiment.
3. On systems where notebook DataLoader multiprocessing fails, start with `num_workers=0`.
4. Restart the kernel and run cells in order. Check the noise schedule, tensor shapes, a training step, and checkpoint loading before a long run.

The dialogue notebook additionally expects CSV files under a Kaggle input directory and imports pandas, tokenizers, and transformers. Review its data paths and dataset terms before running or redistributing its outputs.

## How to interpret the diffusion notebook

- Despite names such as `TextEmbedding` and `sample_from_text`, conditioning is a learned embedding of ten digit IDs. There is no natural-language text encoder.
- The periodic training preview calls an unconditional sampler; final class-specific generation supplies the digit embedding.
- The saved “best” checkpoint uses the last training-batch loss of an epoch. It is not selected on validation quality.
- Saved images and loss logs are qualitative evidence. No FID, classifier-based conditional accuracy, multi-seed analysis, or generalization result is claimed.
- The notebook does not establish seeded, end-to-end reproducibility.

These limits are useful next experiments: a fixed-seed baseline, consistent checkpoint paths, validation-based selection, and a documented conditional-generation evaluation.

## Contribute

See [CONTRIBUTING.md](CONTRIBUTING.md). Small portability fixes, shape checks, training/sampling comparisons, and documented reproductions are welcome. Preserve historical outputs as historical evidence and label newly generated results with their configuration.

No standalone LICENSE file is included. Dataset and source-code reuse terms should be checked separately.
