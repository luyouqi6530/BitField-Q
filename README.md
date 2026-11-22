# BitField-Q — 32-bit A20K model backup

This repository preserves the frozen-Writer A-arm model and its original evaluation outputs. The checkpoint is distributed as a release asset, not stored in Git history.

## Model

- Checkpoint: `step_020000.pt`, stage A, step 20,000.
- Writer: explicit bit-conditioned latent fields.
- Reader: independent GIA, 32-bit RGB blind decoding.
- Writer and VAE frozen during this A-arm Reader continuation.
- The checkpoint contains Writer and Reader state dictionaries, configuration and fixed gain.
- Matching frozen VAE and standalone inference runtime are not yet included. Cloning this backup alone is not sufficient to run inference.

## Frozen P256/M8 retest

| Metric | Value |
|---|---:|
| Clean BA | 99.2752% |
| Clean exact-message recovery | 82.2266% |
| PSNR | 37.4041 dB |
| SSIM | 0.964570 |
| LPIPS | 0.014742 |

Quality is measured against the VAE reconstruction of the same unwatermarked cover latent, not the original RGB image. BA values in the JSON are fractions; CSV columns labeled percent use percentages.

The original preservation guards did not all pass (see `model_manifest.json` and the retest JSON). This release preserves the specified A-arm checkpoint; it does not claim that it was automatically promoted as the globally best model.

## Files

- `model_manifest.json`: checkpoint checksum, size and protocol.
- `training_result.json`: original training final evaluations.
- `retest_result.json`, `attacks.csv`, `quality.csv`: original full retest outputs.
- Release `a20k-backup-v1`: checkpoint and checksum file.

## Check downloaded weights

```bash
sha256sum -c SHA256SUMS.txt
```

This public repository currently provides the model backup and evaluation artifacts. A standalone inference package and the matching VAE are not included yet.
