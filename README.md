# Recommended DINOv3 model checkpoints

This folder contains the recommended `C1_long`, `D1_long`, and `G1_long` checkpoints, their exported configs, and inference settings. It does not include the main repository code, backbone weights, original-run checkpoints, training data, or predictions. Use the existing main repository checkout for model code and dependencies.

The long-run checkpoints contain LoRA/decoder weights and require DINOv3 ViT-L/16 backbone `facebook/dinov3-vitl16-pretrain-lvd1689m` at revision `ea8dc2863c51be0a264bab82070e3e8836b02d51`. The backbone is gated and not bundled; obtain separately authorized access/cache. Historical paths in `config_resolved.json` are provenance only. Override `model_id` at inference time with a local snapshot or HF model ID; use `local_files_only=False` only if download/access is authorized.

## Load and predict

From the main repository's `Code` working directory, use the existing factory. The loader returns `(adapter, identity)`:

    import cv2
    from dino_iml.model.eval_factory import build_dino_model

    adapter, identity = build_dino_model(
        checkpoint_path="/absolute/path/to/DINO_Model_Handoff_2026-11-03/C1_long/checkpoint_best.pt",
        device="cuda",
        model_config={"model_id": "/path/to/dinov3-vitl16", "local_files_only": True},
    )
    scores_512 = adapter.predict(rgb_image)
    scores_native = cv2.resize(
        scores_512,
        (rgb_image.shape[1], rgb_image.shape[0]),
        interpolation=cv2.INTER_LINEAR,
    )
    mask = scores_native > 0.5

Replace the checkpoint path above with the downloaded package or clone location on your machine. Pass an RGB uint8 image. The adapter returns 512×512 sigmoid probabilities; resize the float32 probability map to original `(width, height)` with `cv2.INTER_LINEAR`, then threshold strictly with `score > 0.5`. Do not add morphology, tiling, fusion, or an image-level threshold. No inference was run while preparing this handoff.

## Selection notes

- `C1_long`: five-dataset mean 0.7924 vs original C1 0.7912, a near tie.
- `D1_long`: Testing 0.8047 vs 0.7126; FCD 0.6326 vs 0.5787; SCD 0.7385 vs 0.6413; RTM F1 is lower at 0.0703 vs 0.0731.
- `G1_long`: OpenSDI mean 0.7052 vs original 0.6541; CocoGlide 0.8039 vs 0.8273, a regression.

Selected best epochs are C1 340, D1 20, G1 30 from completed long runs of 10,000, 9,900, and 9,840 attempts. C1 and D1 are best checkpoints, not final-epoch checkpoints. Each model folder contains its comparison note.

## Provenance

`source_provenance.json` records source commit, backbone revision, selected epochs, and checkpoint/config/settings hashes. `checksums.sha256` covers every file in this folder except itself. `.gitattributes` disables line-ending conversion so copied checkpoint/config bytes remain stable. No Git repository is initialized here.
