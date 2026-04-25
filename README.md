# Synapse AgentPay

The first B2A (Business-to-Agent) crypto payment gateway for AI agents.

Synapse AgentPay 是面向 AI Agent 的 B2A（Business-to-Agent）加密支付网关。

[English first, 中文说明紧随其后。](#30-second-agent-quickstart)

[Read the Full Documentation](https://staging.synapse-network.ai/docs) ·
[Python SDK](https://staging.synapse-network.ai/docs/sdk/python) ·
[TypeScript SDK](https://staging.synapse-network.ai/docs/sdk/typescript) ·
[SDK Repository](https://github.com/cliff-personal/Synapse-Network-Sdk)

Synapse lets agents discover services, pay with USDC-priced credentials, invoke APIs, and verify settlement with receipts.

Synapse 让 Agent 可以发现服务、用 USDC 计价凭据完成调用，并通过 receipt 验证结算结果。

## 30-Second Agent Quickstart

30 秒 Agent 快速接入。

Step 1: Get your Agent Key.

步骤 1：获取 Agent Key。

Open the **[Synapse Gateway Dashboard (Testnet Sandbox)](https://staging.synapse-network.ai)**, connect your wallet, and generate an Agent Key that starts with `agt_`.

打开 **[Synapse Gateway Dashboard（测试网沙盒）](https://staging.synapse-network.ai)**，连接钱包，并生成一个以 `agt_` 开头的 Agent Key。

Step 2: Let your agent discover and work.

步骤 2：让 Agent 自动发现服务并开始工作。

```python
from synapse_client import SynapseClient

# Use "staging" for testnet (free), "prod" for mainnet (real USDC).
# 使用 "staging" 连接测试网免费环境，使用 "prod" 连接主网真实 USDC 环境。
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
  // 使用 "staging" 连接测试网免费环境，使用 "prod" 连接主网真实 USDC 环境。
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

运行环境：Staging 与 Production。

Synapse operates on strict environment isolation to protect your funds.

Synapse 采用严格的环境隔离来保护资金安全。

- **Staging (`environment="staging"`)**: Available now. Backed by Arbitrum Sepolia (testnet). Uses MockUSDC. Use this environment to build, test your agents, and verify API workflows for free.
- **Production (`environment="prod"`)**: Pending mainnet launch. Backed by Arbitrum One. Uses real USDC. Currently reserved and locked behind human gates until General Availability (GA).

- **Staging (`environment="staging"`)**：当前可用。基于 Arbitrum Sepolia 测试网，使用 MockUSDC。适合免费构建、测试 Agent，并验证 API 工作流。
- **Production (`environment="prod"`)**：等待主网上线。基于 Arbitrum One，使用真实 USDC。当前为 GA 前保留环境，并受人工安全门控保护。

Note: The Quickstart above uses the `staging` environment. You can switch to `prod` by changing the environment parameter and providing a live Agent Key once production is un-gated.

注意：上面的 Quickstart 默认使用 `staging`。生产环境开放后，只需把 environment 参数切换为 `prod`，并提供正式 Agent Key 即可。

## Why Synapse

为什么选择 Synapse。

- Agent-first runtime: agents use `SynapseClient` and an `agt_xxx` key.
- Discovery before execution: agents search services and read the current price before invoking.
- Settlement evidence: every invocation can be checked with a receipt.
- Staging-first preview: production docs and domains are reserved until GA.

- Agent-first 运行时：Agent 使用 `SynapseClient` 和 `agt_xxx` key。
- 先发现再执行：Agent 在调用前先搜索服务并读取当前价格。
- 可验证结算证据：每次调用都可以通过 receipt 查询结算结果。
- Staging-first 公测：生产文档和域名将在 GA 前保持预留。

## For AI Coding Agents

面向 AI 编码 Agent。

Use [llm-instructions.md](./llm-instructions.md) as the compact integration prompt for Cursor, Copilot, Codex, and other coding agents.

将 [llm-instructions.md](./llm-instructions.md) 作为 Cursor、Copilot、Codex 等编码 Agent 的精简接入提示词。

The most important rule: agent runtime code should use `SynapseClient`, not owner/admin wallet setup.

最重要的规则：Agent 运行时代码应该使用 `SynapseClient`，不要初始化 owner/admin 钱包流程。

## Full Docs

完整文档。

This repository is the GitHub funnel and agent-readable index. The polished product documentation lives on the Gateway docs site:

这个仓库是 GitHub 流量入口和 Agent 可读索引；完整产品化文档在 Gateway docs 站点：

- SDK hub: <https://staging.synapse-network.ai/docs/sdk>
- Python SDK: <https://staging.synapse-network.ai/docs/sdk/python>
- TypeScript SDK: <https://staging.synapse-network.ai/docs/sdk/typescript>
- Concepts: <https://staging.synapse-network.ai/docs/concepts>
- Contracts: <https://staging.synapse-network.ai/docs/contracts>

V1 intentionally does not expose "Edit this page" links from the docs site because this repository is not yet the source of truth for every rendered docs page. Please use GitHub Issues for docs feedback until docs-source sync lands.

V1 暂不在 docs 站点展示 “Edit this page”，因为当前仓库还不是渲染文档页面的唯一源码。文档源码同源完成前，请先通过 GitHub Issues 反馈。

## Feedback

反馈。

- Report docs issues: <https://github.com/cliff-personal/Synapse-Network-Docs/issues>
- Ask in Community / Discussions: <https://github.com/cliff-personal/Synapse-Network-Docs/discussions>
- SDK code and examples: <https://github.com/cliff-personal/Synapse-Network-Sdk>

Credential handling and vulnerability reporting live in the SDK `SECURITY.md`.

凭据处理和漏洞报告请查看 SDK 仓库的 `SECURITY.md`。
