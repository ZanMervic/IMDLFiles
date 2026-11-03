# G1_long

OpenSDI Stable Diffusion 1.5/generative-local-edit long-run best checkpoint. Selected epoch 30; the full run completed 9,840 update attempts. This folder contains the unchanged checkpoint, its embedded training config exported exactly as `config_resolved.json`, and `inference_settings.json`.

Comparison summary: OpenSDI mean 0.7052 vs original 0.6541; CocoGlide 0.8039 vs 0.8273, a regression.

The original run is not bundled. The long-run config JSON was reconstructed from the embedded checkpoint config because the original resolved training JSON was unavailable locally. Historical paths in that config are provenance only. Use the existing main repository loader and override the backbone path as shown in the [repository README](../README.md).
