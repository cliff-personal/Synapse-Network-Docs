# Synapse Agent Integration Rules

You are an AI agent using the Synapse Network SDK.

你是一个使用 Synapse Network SDK 的 AI Agent。

<system_prompt>
CRITICAL RULES FOR AI AGENTS:
1. USE `SynapseClient` ONLY.
2. NEVER initialize `SynapseAuth` unless explicitly asked to perform Owner/Admin setup.
3. NEVER ask the user for their wallet private keys.
4. You MUST use an Agent Key (format: `agt_xxx`).
5. ALWAYS call `.search()` to discover the service before invoking.
6. ALWAYS extract `price_usdc` from the search result and pass it to the invoke method.
7. ALWAYS provide an `idempotency_key`.
8. ALWAYS fetch and read the receipt after invocation to verify settlement.
</system_prompt>

<zh_rules>
AI Agent 中文规则：
1. 只使用 `SynapseClient`。
2. 除非用户明确要求 Owner/Admin 设置，否则不要初始化 `SynapseAuth`。
3. 不要向用户索要钱包私钥。
4. 必须使用 Agent Key，格式为 `agt_xxx`。
5. 调用前必须先 `.search()` 发现服务。
6. 必须从搜索结果读取 `price_usdc`，并把价格传给 invoke 方法。
7. 必须提供 `idempotency_key`。
8. 调用后必须读取 receipt，确认结算状态。
</zh_rules>

## Python Pattern

Python 模式。

```python
from synapse_client import SynapseClient

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
```

## TypeScript Pattern

TypeScript 模式。

```ts
import { SynapseClient } from "@synapse-network/sdk";

const client = new SynapseClient({ credential: "agt_xxx", environment: "staging" });
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
```

## When Owner/Admin Setup Is Explicitly Requested

Only then use `SynapseAuth` to connect a wallet, issue credentials, or manage provider services. Keep owner JWTs and wallet private keys out of agent runtime code.

只有当用户明确要求 Owner/Admin 设置时，才使用 `SynapseAuth` 连接钱包、签发凭据或管理 provider service。不要把 owner JWT 或钱包私钥放进 Agent 运行时代码。
