# Instructions for coding agents

- Treat each checkpoint and its `config_resolved.json` as immutable. Verify SHA-256 values using `source_provenance.json` and `checksums.sha256` before publishing or changing the bundle.
- Use the existing main repository's `dino_iml.model.eval_factory.build_dino_model`; it returns `(adapter, identity)`. Override the historical config `model_id` with an authorized local backbone snapshot or HF ID, and preserve the pinned revision in the checkpoint.
- Pass RGB uint8 input to `adapter.predict`. Resize its 512×512 float32 probabilities to original `(width, height)` with `cv2.INTER_LINEAR` before applying strict `score > 0.5`.
- Do not retrain or add morphology, tiling, fusion, or image-level thresholds. The bundle contains no backbone, training data, or inference outputs.
