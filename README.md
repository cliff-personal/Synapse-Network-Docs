<p align="center">
  <strong>English</strong> · <a href="./README.zh-CN.md">简体中文</a>
</p>

<p align="center">
  <img src="./assets/synapse-network-logo.svg" alt="SynapseNetwork logo" width="460" />
</p>

# SynapseNetwork

AI-native API commerce, payment, and settlement infrastructure for agents.

[Read the Full Documentation](https://staging.synapse-network.ai/docs) ·
[Python SDK](https://staging.synapse-network.ai/docs/sdk/python) ·
[TypeScript SDK](https://staging.synapse-network.ai/docs/sdk/typescript) ·
[SDK Repository](https://github.com/SynapseNetworkAI/Synapse-Network-Sdk)

SynapseNetwork lets agents discover services, call APIs through the platform, pay small USDC-priced amounts through blockchain-backed settlement, and verify every invocation with receipts.

## 30-Second Agent Quickstart

Step 1: Get your Agent Key.

Open the **[Synapse Gateway Dashboard (Testnet Sandbox)](https://staging.synapse-network.ai)**, connect your wallet, and generate an Agent Key that starts with `agt_`.

Step 2: Let your agent discover and work.

```python
from synapse_client import SynapseClient

# Use "staging" for testnet (free), "prod" for mainnet (real USDC).
client = SynapseClient(api_key="agt_xxx", environment="staging")

services = client.search("free", limit=10)
service = services[0]

result = client.invoke(
    service.service_id,
    {"prompt": "hello"},
    cost_usdc=float(service.price_usdc),
    idempotency_key="agent-job-001",
)

receipt = client.get_invocation(result.invocation_id)
print(receipt.invocation_id, receipt.status, receipt.charged_usdc)
```

```ts
import { SynapseClient } from "@synapse-network/sdk";

const client = new SynapseClient({
  credential: "agt_xxx",
  // Use "staging" for testnet (free), "prod" for mainnet (real USDC).
  environment: "staging",
});

const services = await client.search("free", { limit: 10 });
const service = services[0];

const result = await client.invoke(
  service.serviceId ?? service.id!,
  { prompt: "hello" },
  {
    costUsdc: Number(service.pricing?.amount ?? 0),
    idempotencyKey: "agent-job-001",
  }
);

const receipt = await client.getInvocation(result.invocationId);
console.log(receipt.invocationId, receipt.status, receipt.chargedUsdc);
```

## Environments: Staging vs. Production

SynapseNetwork operates on strict environment isolation to protect your funds.

- **Staging (`environment="staging"`)**: Available now. Backed by Arbitrum Sepolia testnet. Uses MockUSDC. Use it to build, test agents, and verify API workflows for free.
- **Production (`environment="prod"`)**: Pending mainnet launch. Backed by Arbitrum One. Uses real USDC. Reserved behind human gates until General Availability.

The Quickstart uses `staging`. Switch to `prod` only after production is un-gated and you have a live Agent Key.

## Why SynapseNetwork

- Agent-first runtime: agents use `SynapseClient` and an `agt_xxx` key.
- Discovery before execution: agents search services and read the current price before invoking.
- Small API payments: agents can pay per invocation instead of relying on large prepaid integrations.
- Blockchain-backed settlement: USDC custody and settlement evidence are anchored through the chain-backed payment layer.
- Receipts: every invocation can be checked after settlement.
- Staging-first preview: production docs and domains remain reserved until GA.

## For AI Coding Agents

Use [llm-instructions.md](./llm-instructions.md) as the compact integration prompt for Cursor, Copilot, Codex, and other coding agents.

The most important rule: agent runtime code should use `SynapseClient`, not owner/admin wallet setup.

## Full Docs

This repository is the GitHub funnel and agent-readable index. The polished product documentation lives on the Gateway docs site:

- SDK hub: <https://staging.synapse-network.ai/docs/sdk>
- Python SDK: <https://staging.synapse-network.ai/docs/sdk/python>
- TypeScript SDK: <https://staging.synapse-network.ai/docs/sdk/typescript>
- Concepts: <https://staging.synapse-network.ai/docs/concepts>
- Contracts: <https://staging.synapse-network.ai/docs/contracts>

V1 intentionally does not expose "Edit this page" links from the docs site because this repository is not yet the source of truth for every rendered docs page. Please use GitHub Issues for docs feedback until docs-source sync lands.

## Feedback

- Report docs issues: <https://github.com/SynapseNetworkAI/Synapse-Network-Docs/issues>
- Ask in Community / Discussions: <https://github.com/SynapseNetworkAI/Synapse-Network-Docs/discussions>
- SDK code and examples: <https://github.com/SynapseNetworkAI/Synapse-Network-Sdk>

Credential handling and vulnerability reporting live in the SDK `SECURITY.md`.
