# Sipsa Labs

> A research lab — Systems · Intelligence · Precision. UltraCompress is our flagship publicly-shipped product.

---

## What we ship publicly

### [UltraCompress](https://github.com/sipsalabs/ultracompress)

Extreme compression infrastructure for large language models. **Per-layer streaming compression** validated end-to-end across the full Qwen scaling curve:

| Model | PPL ratio | Peak VRAM (compress) |
|---|---:|---:|
| Qwen3-8B | 1.0278× | 2.26 GB |
| Qwen3-14B | 1.0111× | 3.37 GB |
| Qwen3-32B | 1.0367× | 4.85 GB |
| **Qwen2.5-72B** | **1.0162×** | **8.98 GB** |

**Qwen2.5-72B compresses to 8.98 GB peak VRAM on a single RTX 5090** — production-grade quality (1.6% PPL drift) on consumer hardware. Peak VRAM is bounded by ~one transformer layer regardless of total model depth, so the same pipeline scales to arbitrary sizes.

```
pip install ultracompress
```

Apache-2.0 CLI. Pre-compressed reference models distributed via the [Hugging Face Hub](https://huggingface.co/sipsalabs) (rolling release through April–May 2026).

Patent pending — USPTO 64/049,511 + 64/049,517, filed April 25, 2026; supplement filing May 2026 covering streaming-compression mechanism.

---

## What's coming

- **v0.1 alpha** — pre-compressed reference models for Qwen3 / Qwen2.5 / Llama / Mistral families, rolling release April–May 2026
- **v0.2 (Q3 2026)** — `uc compress` self-compression of customer models, architectural-compression (FRR / CHBR) variants, native exports to llama.cpp, vLLM, TensorRT-LLM, CoreML
- **v0.3** — composed Track A × Track B × Track C stack toward the 100T-on-one-GPU mission

---

## Contact

- **Pilots / commercial** → founder@sipsalabs.com
- **Patents / licensing** → legal@sipsalabs.com
- **Press / media** → press@sipsalabs.com
- **Security disclosure** → security@sipsalabs.com
- **General** → hello@sipsalabs.com

[sipsalabs.com](https://sipsalabs.com)
