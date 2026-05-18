<p align="center">
  <img src="https://amalgix.io/assets/logo-icon.png" width="80" alt="Amalgix Logo">
</p>

<h1 align="center">Amalgix</h1>

<p align="center">
  <strong>Document Intelligence Engine — MCP + REST + x402 Pay-Per-Call</strong>
</p>

<p align="center">
  <a href="https://amalgix.io">Website</a> •
  <a href="https://amalgix.io/openapi.json">OpenAPI Spec</a> •
  <a href="https://smithery.ai/servers/amalgix/document-intelligence">Smithery</a> •
  <a href="https://www.x402scan.com/server/41885358-75a2-4c56-835e-83180b18d53a">x402scan</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/protocol-MCP-blue" alt="MCP">
  <img src="https://img.shields.io/badge/payment-x402%20USDC-green" alt="x402">
  <img src="https://img.shields.io/badge/chains-Base%20%7C%20Solana-purple" alt="Chains">
  <img src="https://img.shields.io/badge/tools-7-orange" alt="Tools">
  <img src="https://img.shields.io/badge/accuracy-100%25-brightgreen" alt="Accuracy">
</p>

---

## What is Amalgix?

Amalgix is a **production-grade document intelligence API** powered by the proprietary **Crucible™ Engine**. It runs multiple AI models against each other — hallucinations get flagged before they reach you.

- **Up to 56x cheaper** than calling frontier models directly
- **Zero API keys** — pay per call with USDC via x402 protocol
- **Cross-model verification** — no single model can hallucinate unchecked
- **MCP-native + REST API** — works with any AI agent or HTTP client

## Quick Start

### MCP (Recommended)

Add to your MCP client config:

```json
{
  "mcpServers": {
    "amalgix": {
      "url": "https://amalgix.io/mcp",
      "transport": "streamable-http"
    }
  }
}
```

### REST API

```bash
curl -X POST https://amalgix.io/api/health_check
```

All paid endpoints require x402 payment headers. Use `estimate_cost` (free) to preview pricing before any paid call.

### Try It Instantly

```bash
npx agentcash try https://amalgix.io
```

## Tools

| Tool | Description | Pricing |
|:-----|:------------|:--------|
| `analyze_document` | Deep analysis with cross-provider verification. Structured JSON output with findings, evidence, and confidence scores. | Dynamic — from $0.02 |
| `extract_web` | Extract and analyze content from any URL, including JS-rendered pages. | From $0.02 |
| `summarize` | Fast single-pass summarization with key points. Best for short documents. | From $0.01 |
| `delegate_coding` | Generate, review, or extract code. Three modes in one tool. | From $0.02 |
| `delegate_bulk_translate` | Translate all string values in a JSON object. Preserves structure. | From $0.01 |
| `estimate_cost` | **FREE** — Get exact price quote before paying. | Free |
| `health_check` | **FREE** — Check service availability and engine status. | Free |

## How It Works — Crucible™ Pipeline

```
Document → Ingest → Crucible™ Engine → Cross-Verify → Validate → Structured Output
                         ↓                    ↓            ↓
                   Smart Routing      Multi-Model CoVe   Ground Truth
                   (optimal model)    (providers check   (critic vs source)
                                       each other)
```

1. **Ingest** — Document, URL, or raw text up to 20MB. Auto-detected language and format.
2. **Crucible™** — Proprietary multi-stage extraction with intelligent model routing.
3. **Cross-Verify** — Multiple AI providers validate each other's outputs.
4. **Validate** — Critic verifies every finding against the original source text.
5. **Output** — Schema-enforced structured JSON with confidence scores.

## Pricing

Dynamic pricing based on document size. Settled instantly via x402 in USDC.

| Tier | Document Size | Price Range | Routing |
|:-----|:-------------|:------------|:--------|
| L1 — Lightweight | < 128KB | $0.01 – $0.16 | Single Gemini Flash call, ~3s |
| L2 — Standard | 128KB – 3.2MB | $0.16 – $5.77 | Extract + cross-provider verify, ~10–30s |
| L3 — Enterprise | > 3.2MB | $5.77 – $15.00 | Chunked MoA parallel pipeline, ~30s–2min |

**No subscriptions. No API keys. No prepaid credits.**

## Benchmark Results

Tested on real enterprise documents (Samsung, Toyota, Aramco, Inditex, LVMH):

| Metric | Amalgix | GPT-5.5-Pro | Opus 4.7 | Gemini 3.1 Pro |
|:-------|:--------|:------------|:---------|:---------------|
| 5-Dimension Accuracy | **100%** | 100% | 100% | 85.5% |
| 10-Language Accuracy | **100%** | 90.6% | 95.0% | 73.9% |
| Chinese Document | **100%** | 100% | 50% | 27% |
| Arabic + Russian | **100%** | 53% | 100% | 78% |
| Hallucinations | **0** | 0 | 0 | 0 |
| Cost per test | **$0.034** | $1.892 | $0.119 | $0.074 |
| Cost Efficiency vs GPT | **56x** | 1x | 16x | 26x |

## Payment

Amalgix uses the [x402 protocol](https://www.x402.org/) for trustless micropayments:

- **Currency**: USDC
- **Chains**: Base (EVM) or Solana (SVM)
- **Scheme**: `upto` (EVM) / `exact` (SVM)
- **Settlement**: Instant, on-chain

No wallet setup required for agents — x402-compatible clients handle payment automatically.

## Security & Privacy

- **Zero Storage** — Documents processed in volatile memory only, never written to disk
- **Encrypted Transit** — All connections use TLS; no document content in logs
- **Third-Party Processing** — Content is sent to LLM providers (Google, Anthropic) for analysis
- **PII Redaction** — Built-in output guard removes sensitive data from responses

⚠️ Do not submit documents containing passwords, private keys, SSNs, or other regulated PII.

## Links

- 🌐 **Website**: [amalgix.io](https://amalgix.io)
- 📖 **API Docs**: [amalgix.io → Docs](https://amalgix.io/#docs)
- 🔌 **MCP Registry**: [Smithery](https://smithery.ai/servers/amalgix/document-intelligence)
- 💰 **x402 Listing**: [x402scan](https://www.x402scan.com/server/41885358-75a2-4c56-835e-83180b18d53a)
- 📧 **Contact**: contact@amalgix.io

## License

All Rights Reserved © 2026 Amalgix. This repository contains documentation and configuration files only. The Amalgix engine source code is proprietary and not included.
