<p align="center">
  <strong>English</strong> · <a href="./README.zh-CN.md">简体中文</a>
</p>

<p align="center">
  <img src="./assets/synapse-network-logo.svg" alt="SynapseNetwork logo" width="460" />
</p>

# SynapseNetwork

AI-native API commerce, payment, and settlement infrastructure for agents.

[Read the Full Documentation](https://synapse-network.ai/docs) ·
[Python SDK](https://synapse-network.ai/docs/sdk/python) ·
[TypeScript SDK](https://synapse-network.ai/docs/sdk/typescript) ·
[SDK Repository](https://github.com/SynapseNetworkAI/Synapse-Network-Sdk)

SynapseNetwork lets agents discover services, call APIs through the platform, pay small USDC-priced amounts through blockchain-backed settlement, and verify every invocation with receipts.

## 30-Second Agent Quickstart

Step 1: Get your Agent Key.

Open the **[Synapse Gateway Dashboard (Testnet Sandbox)](https://staging.synapse-network.ai)**, connect your wallet, and generate an Agent Key that starts with `agt_`.

Step 2: Let your agent discover and work.

```python
import os

from synapse_client import SynapseClient

# Use "staging" for testnet (free), "prod" for mainnet (real USDC).
client = SynapseClient(api_key=os.environ["SYNAPSE_AGENT_KEY"], environment="staging")

services = client.search("svc_synapse_echo", limit=10)
service = services[0]

result = client.invoke(
    service.service_id,
    {"message": "hello from SynapseNetwork"},
    cost_usdc=str(service.price_usdc),
    idempotency_key="agent-job-001",
)

receipt = client.get_invocation(result.invocation_id)
print(receipt.invocation_id, receipt.status, receipt.charged_usdc)
```

```ts
import { SynapseClient } from "@synapse-network-ai/sdk";

const client = new SynapseClient({
  credential: process.env.SYNAPSE_AGENT_KEY!,
  // Use "staging" for testnet (free), "prod" for mainnet (real USDC).
  environment: "staging",
});

const services = await client.search("svc_synapse_echo", { limit: 10 });
const service = services[0];

const result = await client.invoke(
  service.serviceId ?? service.id!,
  { message: "hello from SynapseNetwork" },
  {
    costUsdc: String(service.pricing?.amount ?? "0"),
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
- Production docs-first discovery with staging as the testnet sandbox.

## For AI Coding Agents

Use [llm-instructions.md](./llm-instructions.md) as the compact integration prompt for Cursor, Copilot, Codex, and other coding agents.

The most important rule: agent runtime code should use `SynapseClient`, not owner/admin wallet setup.

## Full Docs

This repository is the GitHub funnel, agent-readable index, and public-source mirror for docs pages that expose `Open in GitHub`. The polished product documentation still lives on the production docs site:

- SDK hub: <https://synapse-network.ai/docs/sdk>
- Python SDK: <https://synapse-network.ai/docs/sdk/python>
- TypeScript SDK: <https://synapse-network.ai/docs/sdk/typescript>
- Concepts: <https://synapse-network.ai/docs/concepts>
- Contracts: <https://synapse-network.ai/docs/contracts>

Staging remains the public testnet sandbox for first calls and integration tests: <https://staging.synapse-network.ai/docs>.

Preview SDK guides for Go, Java/JVM, and .NET live in the official SDK repository until product docs pages are generated:

- Go SDK: <https://github.com/SynapseNetworkAI/Synapse-Network-Sdk/blob/main/docs/sdk/go_integration.md>
- Java/JVM SDK: <https://github.com/SynapseNetworkAI/Synapse-Network-Sdk/blob/main/docs/sdk/java_integration.md>
- .NET SDK: <https://github.com/SynapseNetworkAI/Synapse-Network-Sdk/blob/main/docs/sdk/dotnet_integration.md>

Public docs pages may link here for source viewing, but V1 still does not expose "Edit this page" flows because this repository is not yet the canonical authoring source for rendered docs. Please use GitHub Issues for docs feedback until docs-source sync lands.

## Feedback

- Report docs issues: <https://github.com/SynapseNetworkAI/Synapse-Network-Docs/issues>
- Ask in Community / Discussions: <https://github.com/SynapseNetworkAI/Synapse-Network-Docs/discussions>
- SDK code and examples: <https://github.com/SynapseNetworkAI/Synapse-Network-Sdk>

Credential handling and vulnerability reporting live in the SDK `SECURITY.md`.
