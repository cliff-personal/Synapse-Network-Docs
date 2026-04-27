<p align="center">
  <a href="./README.md">English</a> · <strong>简体中文</strong>
</p>

<p align="center">
  <img src="./assets/synapse-network-logo.svg" alt="SynapseNetwork logo" width="460" />
</p>

# SynapseNetwork

面向 AI Agent 的 API 调用、支付与结算基础设施。

[阅读完整文档](https://staging.synapse-network.ai/docs) ·
[Python SDK](https://staging.synapse-network.ai/docs/sdk/python) ·
[TypeScript SDK](https://staging.synapse-network.ai/docs/sdk/typescript) ·
[SDK 仓库](https://github.com/cliff-personal/Synapse-Network-Sdk)

SynapseNetwork 让 Agent 可以发现服务、通过平台调用接口、用区块链支持的 USDC 完成小额付款，并通过 receipt 验证每次调用与结算结果。

## 30 秒 Agent 快速接入

步骤 1：获取 Agent Key。

打开 **[Synapse Gateway Dashboard（测试网沙盒）](https://staging.synapse-network.ai)**，连接钱包，并生成一个以 `agt_` 开头的 Agent Key。

步骤 2：让 Agent 自动发现服务并开始工作。

```python
from synapse_client import SynapseClient

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

## 运行环境：Staging 与 Production

SynapseNetwork 采用严格的环境隔离来保护资金安全。

- **Staging (`environment="staging"`)**：当前可用。基于 Arbitrum Sepolia 测试网，使用 MockUSDC。适合免费构建、测试 Agent，并验证 API 工作流。
- **Production (`environment="prod"`)**：等待主网上线。基于 Arbitrum One，使用真实 USDC。当前为 GA 前保留环境，并受人工安全门控保护。

上面的 Quickstart 默认使用 `staging`。生产环境开放后，只需把 environment 参数切换为 `prod`，并提供正式 Agent Key 即可。

## 为什么选择 SynapseNetwork

- Agent-first 运行时：Agent 使用 `SynapseClient` 和 `agt_xxx` key。
- 先发现再执行：Agent 在调用前先搜索服务并读取当前价格。
- 小额 API 付款：Agent 可以按调用粒度付款，而不是依赖大额预付集成。
- 区块链支持结算：USDC 托管与结算证据由链上支付层承载。
- 可验证 receipt：每次调用都可以在结算后查询结果。
- Staging-first 公测：生产文档和域名将在 GA 前保持预留。

## 面向 AI 编码 Agent

将 [llm-instructions.md](./llm-instructions.md) 作为 Cursor、Copilot、Codex 等编码 Agent 的精简接入提示词。

最重要的规则：Agent 运行时代码应该使用 `SynapseClient`，不要初始化 owner/admin 钱包流程。

## 完整文档

这个仓库是 GitHub 流量入口和 Agent 可读索引；完整产品化文档在 Gateway docs 站点：

- SDK hub: <https://staging.synapse-network.ai/docs/sdk>
- Python SDK: <https://staging.synapse-network.ai/docs/sdk/python>
- TypeScript SDK: <https://staging.synapse-network.ai/docs/sdk/typescript>
- Concepts: <https://staging.synapse-network.ai/docs/concepts>
- Contracts: <https://staging.synapse-network.ai/docs/contracts>

V1 暂不在 docs 站点展示 “Edit this page”，因为当前仓库还不是渲染文档页面的唯一源码。文档源码同源完成前，请先通过 GitHub Issues 反馈。

## 反馈

- 反馈文档问题：<https://github.com/cliff-personal/Synapse-Network-Docs/issues>
- 社区讨论：<https://github.com/cliff-personal/Synapse-Network-Docs/discussions>
- SDK 代码与示例：<https://github.com/cliff-personal/Synapse-Network-Sdk>

凭据处理和漏洞报告请查看 SDK 仓库的 `SECURITY.md`。
