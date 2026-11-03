# D1_long

DocTamper/document-domain long-run best checkpoint. Selected epoch 20; the full run completed 9,900 update attempts. This folder contains the unchanged checkpoint, its embedded training config exported exactly as `config_resolved.json`, and `inference_settings.json`.

Comparison summary: Testing 0.8047 vs 0.7126; FCD 0.6326 vs 0.5787; SCD 0.7385 vs 0.6413; RTM F1 is lower at 0.0703 vs 0.0731.

The original run is not bundled. The long-run config JSON was reconstructed from the embedded checkpoint config because the original resolved training JSON was unavailable locally. Historical paths in that config are provenance only. Use the existing main repository loader and override the backbone path as shown in the [repository README](../README.md).
