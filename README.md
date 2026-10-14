# Awesome Inferit

[![Website](https://img.shields.io/badge/inferit.cc-website-141414?labelColor=6B6D71)](https://inferit.cc)
[![Docs](https://img.shields.io/badge/docs-inferit.cc%2Fdocs-141414?labelColor=6B6D71)](https://inferit.cc/docs)
[![X](https://img.shields.io/badge/X-%40inferit__-141414?logo=x&logoColor=ECEAE4&labelColor=6B6D71)](https://x.com/inferit_)
[![License: CC0-1.0](https://img.shields.io/badge/license-CC0--1.0-141414?labelColor=6B6D71)](LICENSE)
[![Links](https://img.shields.io/github/actions/workflow/status/InferitAI/awesome-inferit/links.yml?branch=main&label=links&color=141414&labelColor=6B6D71)](https://github.com/InferitAI/awesome-inferit/actions/workflows/links.yml)

Docs, guides, repositories and live endpoints for [Inferit](https://inferit.cc), in one index. Inferit is a peer-to-peer market for AI inference: anyone can sell inference for any model, at their own price, and buyers and agents pay per request through one OpenAI-compatible API.

> **Status:** Testnet demo on Whitechain Sepolia. Prices settle in Inferit Test Credit (ITC), a test token with no monetary value. The contracts are not audited. Inferit has no token.

## Contents

- [Start here](#start-here)
- [Buy inference](#buy-inference)
- [Agents and x402](#agents-and-x402)
- [Framework and tool guides](#framework-and-tool-guides)
- [Sell inference](#sell-inference)
- [Payments on Whitechain](#payments-on-whitechain)
- [Live API endpoints](#live-api-endpoints)
- [Repositories](#repositories)
- [Security and trust](#security-and-trust)
- [Community](#community)
- [Contributing](#contributing)

## Start here

- [inferit.cc](https://inferit.cc): what Inferit is, with each live model's price against its list price (list prices from an OpenRouter snapshot, 2026-10-02).
- [inferit.app](https://inferit.app): the app. [Buy](https://inferit.app/buy) holds your balance, ceiling, API keys and usage; [Sell](https://inferit.app/sell) holds your machines, offers and prices.
- [Documentation](https://inferit.cc/docs): the overview, units (µ, one micro-dollar) and the two ways to pay.
- [Quickstart](https://inferit.cc/docs/quickstart): from zero to a settled request on Whitechain Sepolia, in the app or by hand.

## Buy inference

- [API reference](https://inferit.cc/docs/api-reference): every endpoint, authentication with an API key or x402, money in µ, errors and response headers.
- [Automatic model routing](https://inferit.cc/docs/routing): how `"model": "auto"` picks a model. Its policies, its hints, and the quality ranking it reads (Artificial Analysis Intelligence Index, read 2026-10-06).
- [Wallet and keys](https://inferit.cc/docs/wallet): one balance, a key per teammate or agent with its own spend limit, the ceiling and its expiry, usage and CSV export.
- [Models with live offers](https://inferit.app/models): the catalog, list prices and the lowest live all-in prices.

The API is OpenAI-compatible. Point any OpenAI client at `https://api-production-c74b9.up.railway.app/v1` with your key, and name a model with a live offer or send `"model": "auto"`. Auto chooses among ranked models that have a healthy seller; when none has one, it answers `503 no_eligible_model` and nothing is charged.

## Agents and x402

- [Inferit for agents](https://inferit.cc/agents): how an agent buys inference per request, with no account and no API key.
- [agents.md](https://inferit.cc/agents.md): the same guide for machines: model auto, x402 v2 pay per request, limits, errors and the ITC faucet.
- [llms.txt](https://inferit.cc/llms.txt) and [llms-full.txt](https://inferit.cc/llms-full.txt): the site and docs for language models. Every page on inferit.cc also has a markdown twin: add `.md` to its path.
- [x402 discovery](https://api-production-c74b9.up.railway.app/.well-known/x402): what a client signs for: network, asset, payee and the minimum amount (10 000 µ, that is 0.01 ITC).

A call with no key gets `402 Payment Required` with a quote. The agent signs an EIP-3009 authorization, resends the same body with the `PAYMENT-SIGNATURE` header, and is charged the metered cost; the rest stays its escrow balance.

## Framework and tool guides

- [LangChain](https://inferit.cc/docs/guides/langchain): Python and JavaScript, model auto or a named model, and x402 from LangChain JS.
- [Vercel AI SDK](https://inferit.cc/docs/guides/vercel-ai-sdk): Inferit's base URL and key in the AI SDK's OpenAI-compatible setup, and x402 through a custom fetch.
- [LiteLLM](https://inferit.cc/docs/guides/litellm): the SDK call with the `openai/` prefix, and a proxy config.
- [CrewAI](https://inferit.cc/docs/guides/crewai): Inferit as the model of CrewAI agents.
- [OpenCode](https://inferit.cc/docs/guides/opencode): Inferit as a custom OpenAI-compatible endpoint in OpenCode, with model auto or a named model.
- [Cursor](https://inferit.cc/docs/guides/cursor): Inferit models through Cursor's OpenAI base URL override.

## Sell inference

- [Sell from your own PC in 10 minutes](https://inferit.cc/docs/sellers/quickstart): run a model in Ollama or LM Studio, connect it with one command, set a price and list it. The 10 minutes assume the model is already downloaded and your wallet is registered as a seller.
- [Selling inference](https://inferit.cc/docs/sellers): licences, registration, health checks, availability and payouts to your own wallet (test ITC on the testnet).
- [inferit-seller](https://github.com/InferitAI/inferit-seller): the open-source seller app (Apache-2.0, [on npm](https://www.npmjs.com/package/inferit-seller)). It finds Ollama, LM Studio, vLLM or llama.cpp and dials out to the market, so you need no open port and no domain.

```bash
npx -y inferit-seller connect --token icn_… && npx -y inferit-seller install-service
```

The token comes from **Add a machine** in the [Sell workspace](https://inferit.app/sell). Buyers pay your price plus a 5% platform fee, and you are paid per request to the payout wallet you register.

## Payments on Whitechain

- [Whitechain escrow](https://inferit.cc/docs/payments/whitechain): how `MarketEscrow` bounds what can be settled from a buyer, how x402 payments credit the signer, who pays gas, and the live parameters.
- [whitechain-x402-facilitator](https://github.com/InferitAI/whitechain-x402-facilitator): the first public x402 v2 facilitator for Whitechain, live on Whitechain Sepolia (testnet). Apache-2.0. Its live service is at [x402-facilitator-production-ff5f.up.railway.app](https://x402-facilitator-production-ff5f.up.railway.app).
- [awesome-x402-whitechain](https://github.com/InferitAI/awesome-x402-whitechain): x402 on Whitechain, in one list.
- [Whitechain Sepolia explorer](https://explorer.testnet.whitechain.io): every settlement batch and x402 payment, as public chain data.

Inferit runs both facilitators: the one inside the market API and the open-source one, which the market API does not use.

## Live API endpoints

Base URL: `https://api-production-c74b9.up.railway.app`

| Endpoint | What you get |
|---|---|
| [`GET /health`](https://api-production-c74b9.up.railway.app/health) | The network, the `MarketEscrow` contract, and the state of the settlement and x402 keys |
| [`GET /v1/models`](https://api-production-c74b9.up.railway.app/v1/models) | The model auto rows, then the catalog with list prices and the lowest live all-in prices |
| [`GET /v1/routing`](https://api-production-c74b9.up.railway.app/v1/routing) | The auto policies, the hints, the quality ranking and the models auto can choose from now |
| [`GET /.well-known/x402`](https://api-production-c74b9.up.railway.app/.well-known/x402) | The x402 requirement a client signs for |
| [`GET /metrics`](https://api-production-c74b9.up.railway.app/metrics) | Settlement and chain figures, including the settlement cadence |
| [`GET /llms.txt`](https://api-production-c74b9.up.railway.app/llms.txt) | The API's own summary for language models |
| `POST /v1/chat/completions` | Chat completions, streaming included, with an API key or x402 |

## Repositories

| Repository | What it is |
|---|---|
| [inferit-seller](https://github.com/InferitAI/inferit-seller) | Sell inference from your own computer with one command. Apache-2.0, on npm |
| [whitechain-x402-facilitator](https://github.com/InferitAI/whitechain-x402-facilitator) | The first public x402 v2 facilitator for Whitechain, live on Whitechain Sepolia (testnet). Apache-2.0 |
| [inferit-examples](https://github.com/InferitAI/inferit-examples) | Runnable examples for LangChain, the Vercel AI SDK, LiteLLM, CrewAI and OpenCode, paying with an API key or x402 |
| [inferit-agent-example](https://github.com/InferitAI/inferit-agent-example) | A minimal TypeScript agent that pays Inferit per request with x402: no account and no API key |
| [model-catalog](https://github.com/InferitAI/model-catalog) | The models the Inferit API knows, as open data: ids, aliases, context windows and licence classes (CC BY 4.0) |
| [awesome-x402-whitechain](https://github.com/InferitAI/awesome-x402-whitechain) | x402 resources for Whitechain: the spec, SDKs, EIP-3009, the testnet, facilitators and examples |
| [branding](https://github.com/InferitAI/branding) | The Inferit logo files, colours, type and usage rules |

Inferit runs the market API and the router; their code is private.

## Security and trust

- [Security & trust](https://inferit.cc/docs/security-trust): what `MarketEscrow` is designed to enforce, what the API keeps private, what is public on chain, and what is not verified yet.
- [Security policy](https://inferit.cc/security): how to report a vulnerability, what is in scope, and the terms for good-faith research.

The API stores token counts and costs, never prompts or completions. The seller that serves a request does see it.

## Community

- [X: @inferit_](https://x.com/inferit_)
- [About](https://inferit.cc/about): the team and how to reach us.

## Roadmap

- [Inferit roadmap](https://github.com/InferitAI/roadmap) - What is live, what is next and what is planned, one issue per item.

## Contributing

Add one line per resource, in the section it belongs to, with a link that resolves and a description that says what it does. Only public resources that work with Inferit today. Open a pull request; the link check runs on it. By contributing, you dedicate your contribution to the public domain under CC0 1.0.

## License

[CC0 1.0 Universal](LICENSE): the list is dedicated to the public domain. The Inferit name and logo are not covered: see [InferitAI/branding](https://github.com/InferitAI/branding).
