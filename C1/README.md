# C1_long

CASIA2/classical-domain long-run best checkpoint. Selected epoch 340; the full run completed 10,000 update attempts. This folder contains the unchanged checkpoint, its embedded training config exported exactly as `config_resolved.json`, and `inference_settings.json`.

Comparison summary: five-dataset mean 0.7924 vs original C1 0.7912, a near tie.

The original run is not bundled. The long-run config JSON was reconstructed from the embedded checkpoint config because the original resolved training JSON was unavailable locally. Historical paths in that config are provenance only. Use the existing main repository loader and override the backbone path as shown in the [repository README](../README.md).
