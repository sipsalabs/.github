# Sipsa Labs

> **Sipsa Labs, Inc.** — an experimental and deep tech-and-software company. We invent and ship across the full breadth of tech and software: deep research, runtime systems, novel substrates, infrastructure, hardware-adjacent stacks, and software products that don't fit anywhere else yet. **UltraCompress** — lossless 5-bit transformer compression — is our first flagship publicly-shipped product. More products in flight.

> 🔥 **Live on Hacker News today (2026-05-11):** [news.ycombinator.com/item?id=48099107](https://news.ycombinator.com/item?id=48099107)

---

## First flagship product: [UltraCompress](https://github.com/sipsalabs/ultracompress)

**Lossless 5-bit transformer compression.** SHA-256 verifiable bit-identical reconstruction at customer load. Different contract than every other 4–5 bit library: we don't target a quality threshold ("sub-1% PPL drift"), we target a **reconstruction contract** — the customer artifact reproduces exactly the dequantized weight the trainer measured during distillation. If anything drifts, `uc verify` fails loudly.

### This week's verified PPL ratios (5 bpw vs bf16, FineWeb-edu held-out tail, seq_len=1024, seed=42)

| Model | Class | PPL ratio | HF artifact |
|---|---|---:|---|
| Hermes-3-Llama-3.1-405B | First 405B-class lossless 5-bit on a single 32 GB consumer GPU | **1.0066×** | [SipsaLabs/hermes-3-llama-3.1-405b-uc-v3-bpw5](https://huggingface.co/SipsaLabs/hermes-3-llama-3.1-405b-uc-v3-bpw5) |
| Mixtral-8x7B (47B MoE) | Tightest MoE result | **1.00368×** | SipsaLabs/mixtral-8x7b-v0.1-uc-v3-bpw5 |
| Qwen3-1.7B-Base | Tightest dense floor | **1.00401×** | SipsaLabs/qwen3-1.7b-base-uc-v3-bpw5 |
| Qwen3-14B | 14B-class | **1.00403×** | SipsaLabs/qwen3-14b-uc-v3-bpw5 |
| Qwen3-8B | 8B-class | **1.00440×** | SipsaLabs/qwen3-8b-uc-v3-bpw5 |
| Mistral-7B-v0.3 | New this week — 9.16× tighter than prior public best | **1.00548×** | SipsaLabs/mistral-7b-v0.3-uc-v3-bpw5 |
| Phi-3-mini-4k-instruct | Cross-arch confirm | **1.00624×** | SipsaLabs/phi-3-mini-4k-instruct-uc-v3-bpw5 |

22 architectures verified end-to-end (0.6B → 405B, dense + Mixture-of-Experts + state-space). Full matrix at [huggingface.co/SipsaLabs](https://huggingface.co/SipsaLabs).

### Try it (3 commands)

```bash
pip install ultracompress
hf download SipsaLabs/qwen3-1.7b-base-uc-v3-bpw5 --local-dir ./pack
uc verify ./pack
```

### Or use the OpenAI-compatible API (no install)

```bash
export OPENAI_BASE_URL=https://api.sipsalabs.com/v1
curl $OPENAI_BASE_URL/models
```

The official `openai` Python SDK works unchanged — same `client.chat.completions.create()`, same SSE chunks. Backed by dual RTX 5090 over Cloudflare Tunnel.

### License + IP

- **PyPI v0.6+** under [BUSL-1.1](https://github.com/sipsalabs/ultracompress/blob/main/LICENSE) with **Additional Use Grant**: free for sub-$1M ARR companies, research, and individuals. Auto-converts to Apache 2.0 four years after each release.
- **v0.5.x** stays under Apache-2.0 forever on the `legacy/0.5.x` branch.
- USPTO provisionals **64/049,511** + **64/049,517** filed 2026-04-25. Supplement filing landed 2026-05-09. Continuations through 2027.

---

## What's next

- More products in flight across runtime systems, novel substrates, software infrastructure (announced as they ship — we don't pre-announce).
- Continued architecture coverage on UltraCompress: 70B/235B/685B in the queue.
- Public NeurIPS 2026 + ICLR 2027 paper drafts.

---

## Contact

- **Commercial / Phase 0 POC** → founder@sipsalabs.com
- **Patents / licensing** → legal@sipsalabs.com
- **Press / media** → press@sipsalabs.com
- **Security disclosure** → security@sipsalabs.com
- **General** → hello@sipsalabs.com

[sipsalabs.com](https://sipsalabs.com) · [HuggingFace](https://huggingface.co/SipsaLabs) · [PyPI](https://pypi.org/project/ultracompress/) · [Hacker News (live today)](https://news.ycombinator.com/item?id=48099107)
