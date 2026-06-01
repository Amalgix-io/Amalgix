<p align="center">
  <img src="https://amalgix.io/assets/logo-icon.png" width="80" alt="Amalgix Logo">
</p>

<h1 align="center">Amalgix</h1>

<p align="center">
  <strong>Cross-Model Evidence Pipeline for Financial Filings & Contracts</strong><br>
  <em>MCP + REST · x402 Pay-Per-Call · Up to 3.8x cheaper than calling frontier models directly</em>
</p>

<p align="center">
  <a href="https://amalgix.io">Website</a> |
  <a href="https://amalgix.io/openapi.json">OpenAPI Spec</a> |
  <a href="https://smithery.ai/servers/amalgix/document-intelligence">Smithery</a> |
  <a href="https://www.x402scan.com/server/41885358-75a2-4c56-835e-83180b18d53a">x402scan</a> |
  <a href="https://x.com/AmalgixHQ">X (Twitter)</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/protocol-MCP-blue" alt="MCP">
  <img src="https://img.shields.io/badge/payment-x402%20USDC-green" alt="x402">
  <img src="https://img.shields.io/badge/chains-Base%20%7C%20Solana-purple" alt="Chains">
  <img src="https://img.shields.io/badge/tools-8-orange" alt="Tools">
  <img src="https://img.shields.io/badge/output-evidence--backed-brightgreen" alt="Evidence backed">
</p>

---

## Why Amalgix?

AI agents that need evidence-backed facts from financial filings and contracts face a problem: calling frontier models like Opus 4.8 or GPT-5.5 is expensive, and a single call doesn't produce verified evidence — you need at least two passes (extract + verify) to get source-grounded output.

**Amalgix solves this with a cross-model evidence pipeline:**

1. **Model A extracts** — A specialized extraction model pulls structured findings from your document. Each claim is tied to a verbatim quote, confidence score, and source reference.
2. **Model B verifies** — A different model cross-checks every finding against the original source. Contradictions are flagged; unsupported claims are marked for review — not presented as facts.
3. **You pay less** — Because each stage uses the optimal model for the job (not the most expensive one), the total pipeline cost is significantly lower than running frontier models yourself.

### Cost Comparison (1MB Document)

| Provider | Pipeline Cost | vs Amalgix |
|:---------|:-------------|:-----------|
| **Amalgix** | **$0.82** | — |
| Opus 4.8 (2-pass) | $2.88 | 3.5x more |
| GPT-5.5 (2-pass) | $3.12 | 3.8x more |

> Competitor costs represent what it takes to replicate Amalgix's extract → verify output using those models directly (2-pass, ~15% + ~10% output ratio).

## What is Amalgix?

A crypto-native, MCP + REST intelligence API for AI agents. The proprietary **Crucible™ Evidence Engine** orchestrates the cross-model pipeline:

- **Source-grounded claims** — each material finding includes `claim`, `evidence`, `sourceRef`, `confidence`, and `verificationStatus`
- **Cross-model verification** — extraction and verification use different models, catching errors that single-model approaches miss
- **Financial Filing Intelligence** — SEC 10-K, 10-Q, and 20-F analysis by content, filing URL, ticker, or CIK
- **Contract Risk Intelligence** — clauses, obligations, deadlines, liability, missing terms, and evidence
- **x402 payments** — paid calls settle in USDC on Base or Solana. No API keys required, no subscriptions
- **Wallet dashboard** — EVM wallet login for request history and API key management

Crucible is designed for evidence triage and agent workflows. It does not claim perfect accuracy, legal advice, or investment advice; responses expose confidence and verification metadata so downstream systems can inspect the basis for each finding.

## Quick Start

### MCP

Add Amalgix to any Streamable HTTP MCP-compatible client:

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

### REST

```bash
curl -X GET https://amalgix.io/api/v1/health
```

Paid endpoints require x402 payment headers. Use `estimate_cost` first to preview pricing before any paid call.

## Tools

| Tool | Description | Pricing |
|:-----|:------------|:--------|
| `analyze_public_filing` | Financial Filing Intelligence for public SEC filings. Accepts content, filingUrl, ticker, or CIK for 10-K, 10-Q, and 20-F workflows. | $0.03-$79.00 |
| `review_contract_risks` | Contract Risk Intelligence for clauses, obligations, liability exposure, missing clauses, unusual terms, evidence, and human-review flags. Not legal advice. | $0.03-$79.00 |
| `analyze_document` | General evidence analysis with source-grounded findings, confidence, and verification status. | $0.03-$79.00 |
| `extract_web` | Static/server-rendered public web content extraction with optional analysis. | From $0.01 |
| `summarize` | Fast single-pass summarization with key points. | From $0.01 |
| `delegate_bulk_translate` | Translate JSON string values while preserving object structure. | From $0.01 |
| `estimate_cost` | Free pre-flight cost preview for paid tools or workflows. | Free |
| `health_check` | Free service health and engine availability check. | Free |

## REST Endpoints

| Endpoint | Method | Purpose |
|:---------|:-------|:--------|
| `/api/v1/filings/analyze` | POST | Financial Filing Intelligence |
| `/api/v1/contracts/review` | POST | Contract Risk Intelligence |
| `/api/v1/analyze` | POST | General Crucible™ evidence analysis |
| `/api/v1/cost` | POST | Cost estimation, free |
| `/api/v1/health` | GET | Health check, free |
| `/api/v1/auth/evm/nonce` | POST | Create wallet-login challenge, free |
| `/api/v1/auth/evm/verify` | POST | Verify wallet signature, free |
| `/api/v1/api-keys` | GET/POST | List or create API keys after wallet login, free |
| `/api/v1/jobs` | GET | Recent analysis jobs after wallet login, free |
| `/api/v1/requests` | GET | Recent request logs after wallet login, free |
| `/api/v1/payments` | GET | Recent x402 payment events after wallet login, free |

> **Legacy REST tools** (`/api/v1/extract`, `/api/v1/summarize`, `/api/v1/translate`) are available as operator opt-in via `AMALGIX_ENABLE_LEGACY_REST_TOOLS=true`. They remain accessible through MCP by default.

## Crucible™ Output Contract

Crucible normalizes evidence into a stable shape for agents:

```json
{
  "analysis": {
    "summary": "...",
    "evidenceFindings": [
      {
        "claim": "...",
        "evidence": "...",
        "sourceRef": "document:line:12",
        "confidence": "high",
        "verificationStatus": "supported"
      }
    ],
    "overallConfidence": "high"
  },
  "meta": {
    "engine": "Crucible™ Evidence Engine",
    "analysisType": "general_evidence",
    "routingTier": "large_context",
    "estimatedCost": 0.03
  }
}
```

Analysis modes:

- `general_evidence`
- `financial_filing`
- `contract_review`

## Pricing

Dynamic pricing based on document size. Amalgix's cross-model pipeline delivers equivalent evidence quality at a fraction of single-model cost:

| File Size | Amalgix | Opus 4.8 (2-pass) | GPT-5.5 (2-pass) | Savings |
|:----------|:--------|:-------------------|:-------------------|:--------|
| 256KB | $0.30 | $0.76 | $0.82 | 59-62% |
| 1MB | $0.82 | $2.88 | $3.12 | 72-74% |
| 5MB | $7.36 | $12.12 | $13.14 | 39-44% |
| 20MB | $29.42 | $46.52 | $50.50 | 37-42% |

Use the free `estimate_cost` tool for a request-specific quote.

## Payment

Amalgix uses the [x402 protocol](https://www.x402.org/) for pay-per-call settlement:

- **Currency**: USDC
- **Chains**: Base (EVM) or Solana (SVM)
- **Scheme**: `exact`
- **Authentication**: x402 for paid execution; optional wallet/API key identity for dashboard and REST attribution

## Security & Privacy

- Contract raw text is not persisted by default; Amalgix stores hashes, metadata, job status, and optional results only when configured.
- Public financial filing metadata may be cached because filings are public.
- Connections use TLS.
- Paid analysis content is sent to third-party LLM providers for processing.
- Do not submit passwords, private keys, SSNs, classified data, or other regulated PII.
- Contract and filing outputs are evidence triage only, not legal or investment advice.

## Links

- **Website**: [amalgix.io](https://amalgix.io)
- **API Docs**: [amalgix.io/#docs](https://amalgix.io/#docs)
- **OpenAPI**: [amalgix.io/openapi.json](https://amalgix.io/openapi.json)
- **MCP Registry**: [Smithery](https://smithery.ai/servers/amalgix/document-intelligence)
- **x402 Listing**: [x402scan](https://www.x402scan.com/server/41885358-75a2-4c56-835e-83180b18d53a)
- **Official X**: [@AmalgixHQ](https://x.com/AmalgixHQ)
- **Contact**: contact@amalgix.io

## License

All Rights Reserved (c) 2026 Amalgix. This repository contains documentation and configuration files only. The Amalgix engine source code is proprietary and not included.
