<p align="center">
  <a href="./README.md">English</a> · <strong>简体中文</strong>
</p>

<p align="center">
  <img src="./assets/synapse-network-logo.svg" alt="SynapseNetwork logo" width="460" />
</p>

# SynapseNetwork

面向 AI Agent 的 API 调用、支付与结算基础设施。

[阅读完整文档](https://docs.synapse-network.ai/) ·
[Python SDK](https://docs.synapse-network.ai/sdks/python) ·
[TypeScript SDK](https://docs.synapse-network.ai/sdks/typescript) ·
[SDK 仓库](https://github.com/SynapseNetworkAI/Synapse-Network-Sdk)

SynapseNetwork 让 Agent 可以发现服务、通过平台调用接口、用区块链支持的 USDC 完成小额付款，并通过 receipt 验证每次调用与结算结果。

## 30 秒 Agent 快速接入

步骤 1：获取 Agent Key。

打开 **[Synapse Dashboard](https://www.synapse-network.ai)**，连接钱包，并生成一个以 `agt_` 开头的 Agent Key。

步骤 2：让 Agent 自动发现服务并开始工作。

```python
import os

from synapse_client import SynapseClient

# 使用 "staging" 连接测试网免费环境，使用 "prod" 连接主网真实 USDC 环境。
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
  // 使用 "staging" 连接测试网免费环境，使用 "prod" 连接主网真实 USDC 环境。
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
- 以生产文档作为主要发现入口，同时保留 staging 作为测试网沙盒。

## 面向 AI 编码 Agent

将 [llm-instructions.md](./llm-instructions.md) 作为 Cursor、Copilot、Codex 等编码 Agent 的精简接入提示词。

最重要的规则：Agent 运行时代码应该使用 `SynapseClient`，不要初始化 owner/admin 钱包流程。

## 完整文档

这个仓库是 GitHub 流量入口、Agent 可读索引，以及公开文档源码镜像仓；完整产品化文档仍然在生产文档站点：

- SDK hub: <https://docs.synapse-network.ai/sdks>
- Python SDK: <https://docs.synapse-network.ai/sdks/python>
- TypeScript SDK: <https://docs.synapse-network.ai/sdks/typescript>
- Concepts: <https://docs.synapse-network.ai/concepts/agent-settlement>
- Contracts: <https://docs.synapse-network.ai/smart-contracts>

更多 SDK 指南位于生产文档站：

- Go SDK: <https://docs.synapse-network.ai/sdks/go>
- Java/JVM SDK: <https://docs.synapse-network.ai/sdks/java>
- .NET SDK: <https://docs.synapse-network.ai/sdks/dotnet>

公开 docs 页面可以把 “Open in GitHub” 指向这里做源码查看，但 V1 暂不展示 “Edit this page”，因为当前仓库还不是渲染文档页面的唯一权威源码。文档源码同源完成前，请先通过 GitHub Issues 反馈。

## 反馈

- 反馈文档问题：<https://github.com/SynapseNetworkAI/Synapse-Network-Docs/issues>
- 社区讨论：<https://github.com/SynapseNetworkAI/Synapse-Network-Docs/discussions>
- SDK 代码与示例：<https://github.com/SynapseNetworkAI/Synapse-Network-Sdk>

凭据处理和漏洞报告请查看 SDK 仓库的 `SECURITY.md`。
