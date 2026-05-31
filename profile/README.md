# Sipsa Labs

**The efficiency layer for AI.** We build compression and systems that fit any
model onto the hardware you already have — near-losslessly, and with
reconstruction you can verify.

### UltraCompress — our flagship
Near-lossless 5-bit transformer compression (~1% perplexity cost; the 5-bit pack
is lossy) with reproducible, **SHA-256-verifiable reconstruction to the validated
artifact** — a deterministic decode back to the exact quantized weights we
evaluated, **not bit-identical to the original bf16 model**. A 405B-parameter
model runs end-to-end on a single 32 GB consumer GPU at a **1.0066× perplexity ratio**.

```bash
pip install ultracompress
```

### What''s live
- **UltraCompress** — the compression engine (public CLI on PyPI).
- **Sipsa Inference** — OpenAI-compatible API serving compressed weights (api.sipsalabs.com/v1).
- **Compression-as-a-Service** — bring a model, get a verified pack you run yourself.

### Verified
**23 architectures** verified end-to-end (22 PPL-verified + 1 ViT cosine; 0.6B–405B;
dense + MoE + SSM + ViT) — reproducible public artifacts, not internal benchmarks.
Hermes-3-Llama-3.1-405B reconstructs at **1.0066×** on a single 32 GB GPU.

### Why it matters
Models are outgrowing the hardware that runs them. Whoever makes any model run
anywhere — cheaper, faster, provably intact — becomes the layer every AI
deployment passes through. We start where verifiable quality is non-negotiable,
and expand outward.

Built in public while the patents are pending. BUSL-1.1 — free for sub-$1M ARR + research.

**Commercial:** founder@sipsalabs.com · [sipsalabs.com](https://sipsalabs.com) · [PyPI](https://pypi.org/project/ultracompress/)