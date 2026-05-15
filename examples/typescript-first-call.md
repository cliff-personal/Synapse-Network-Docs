# TypeScript First Call

Use this when the developer or AI agent already has an Agent Key from the Synapse Gateway Dashboard.

当开发者或 AI Agent 已经从 Synapse Gateway Dashboard 获取 Agent Key 时，使用这个示例。

```bash
npm install @synapse-network-ai/sdk
export SYNAPSE_ENV=staging
export SYNAPSE_AGENT_KEY=agt_xxx
```

```ts
import { SynapseClient } from "@synapse-network-ai/sdk";

const client = new SynapseClient({
  credential: process.env.SYNAPSE_AGENT_KEY!,
  // Use "staging" for testnet (free), "prod" for mainnet (real USDC).
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

Full runbook: https://docs.synapse-network.ai/sdks/typescript

完整接入手册：https://docs.synapse-network.ai/sdks/typescript
