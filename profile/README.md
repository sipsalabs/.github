# Sipsa Labs

> **Sipsa Labs, Inc.** — an experimental and deep tech-and-software company. We invent and ship across the full breadth of tech and software: deep research, runtime systems, novel substrates, infrastructure, hardware-adjacent stacks, and software products that don't fit anywhere else yet.

> **Two products live today**: **UltraCompress** (lossless 5-bit transformer compression — flagship) and **Sipsa Inference** (OpenAI-compatible serving for our compressed weights). **Compression-as-a-Service** engagements are open. More products in flight — we don't pre-announce.

---

## Product 1: [UltraCompress](https://github.com/sipsalabs/ultracompress) — lossless 5-bit transformer compression

**The flagship.** SHA-256 verifiable bit-identical reconstruction at customer load. Different contract than every other 4–5 bit library: we don't target a quality threshold ("sub-1% PPL drift"), we target a **reconstruction contract** — the customer artifact reproduces exactly the dequantized weight the trainer measured during distillation. If anything drifts, `uc verify` fails loudly.

**v0.6.9 shipped 2026-05-15** — RCE-class fix on `torch.load()` paths + MANIFEST-scrubbed sdist. v0.6.7 + v0.6.8 yanked from PyPI. Upgrade: `pip install --upgrade ultracompress`.

### This week's verified PPL ratios (5 bpw vs bf16, FineWeb-edu held-out tail, seq_len=1024, seed=42)

| Model | Class | PPL ratio | HF artifact |
|---|---|---:|---|
| Hermes-3-Llama-3.1-405B | First 405B-class lossless 5-bit on a single 32 GB consumer GPU | **1.0066×** | [SipsaLabs/hermes-3-llama-3.1-405b-uc-v3-bpw5](https://huggingface.co/SipsaLabs/hermes-3-llama-3.1-405b-uc-v3-bpw5) |
| Mixtral-8x7B (47B MoE) | Tightest MoE result | **1.00368×** | SipsaLabs/mixtral-8x7b-v0.1-uc-v3-bpw5 |
| Qwen3-1.7B-Base | Tightest dense floor | **1.00401×** | SipsaLabs/qwen3-1.7b-base-uc-v3-bpw5 |
| Qwen3-14B | 14B-class | **1.00403×** | SipsaLabs/qwen3-14b-uc-v3-bpw5 |
| Qwen3-8B | 8B-class | **1.00440×** | SipsaLabs/qwen3-8b-uc-v3-bpw5 |
| Mistral-7B-v0.3 | **New this week** — tightest dense 7B-class lossless 5-bit on the public HF Hub | **1.00548×** | SipsaLabs/mistral-7b-v0.3-uc-v3-bpw5 |
| Phi-3-mini-4k-instruct | Cross-arch confirm | **1.00624×** | SipsaLabs/phi-3-mini-4k-instruct-uc-v3-bpw5 |

22 architectures verified end-to-end (0.6B → 405B, dense + Mixture-of-Experts + state-space). Full matrix at [huggingface.co/SipsaLabs](https://huggingface.co/SipsaLabs).

### Try it (3 commands)

```bash
pip install ultracompress
hf download SipsaLabs/qwen3-1.7b-base-uc-v3-bpw5 --local-dir ./pack
uc verify ./pack
```

---

## Product 2: [Sipsa Inference](https://sipsalabs.com/inference) — OpenAI-compatible serving for our compressed weights

**Drop-in replacement for OpenAI's `base_url`.** Same `openai` Python SDK works unchanged — same `client.chat.completions.create()`, same SSE chunks. Backed by dual RTX 5090 over Cloudflare Tunnel.

```bash
export OPENAI_BASE_URL=https://api.sipsalabs.com/v1
curl $OPENAI_BASE_URL/models
```

**Pricing**: Free $5 credit on signup (no card). **Pro $99/mo** (600 RPM, $100 included credit). **Team $499/mo** (2400 RPM, $500 included credit). Full pricing + bill estimator at [sipsalabs.com/pricing](https://sipsalabs.com/pricing).

22 models live in the catalog with `sipsa-*` prefix (e.g. `model="sipsa-hermes-3-llama-3.1-405b"`).

---

## Service: Compression-as-a-Service (CaaS)

Bring a model, we deliver a verified-lossless 5-bit pack you can run on your hardware. **Phase 0 POC** is $5K / 5 business days / customer-picked model. Day 7 deliverable is a pack you self-verify with `uc verify` + benchmark with `uc bench`. Acceptance gate is `uc verify PASS` + PPL ratio within 1.5% on your eval set. Email founder@sipsalabs.com.

---

## License + IP

- **PyPI v0.6+** under [BUSL-1.1](https://github.com/sipsalabs/ultracompress/blob/main/LICENSE) with **Additional Use Grant**: free for sub-$1M ARR companies, research, and individuals. Auto-converts to Apache 2.0 four years after each release.
- **v0.5.x** stays under Apache-2.0 forever on the `legacy/0.5.x` branch.
- Codec internals patent-protected (USPTO provisionals filed 2026-04-25; supplement filing landed 2026-05-09; continuations through 2027).

---

## What's next

- Continued architecture coverage on UltraCompress: 70B / 235B / 685B in the queue.
- Verifier-as-a-Service product (Q3 2026 roadmap).
- Public NeurIPS 2026 + ICLR 2027 paper drafts.

---

## Contact

- **Commercial / Phase 0 POC** → founder@sipsalabs.com
- **Patents / licensing** → legal@sipsalabs.com
- **Press / media** → press@sipsalabs.com
- **Security disclosure** → security@sipsalabs.com
- **General** → hello@sipsalabs.com

[sipsalabs.com](https://sipsalabs.com) · [HuggingFace](https://huggingface.co/SipsaLabs) · [PyPI](https://pypi.org/project/ultracompress/) · [Pricing](https://sipsalabs.com/pricing)
