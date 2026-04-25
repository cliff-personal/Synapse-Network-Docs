# TypeScript First Call

Use this when the developer or AI agent already has an Agent Key from the Synapse Gateway Dashboard.

```bash
npm install @synapse-network/sdk
export SYNAPSE_ENV=staging
export SYNAPSE_API_KEY=agt_xxx
```

```ts
import { SynapseClient } from "@synapse-network/sdk";

const client = new SynapseClient({
  credential: process.env.SYNAPSE_API_KEY!,
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

Full runbook: https://staging.synapse-network.ai/docs/sdk/typescript
