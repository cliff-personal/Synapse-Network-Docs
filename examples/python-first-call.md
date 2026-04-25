# Python First Call

Use this when the developer or AI agent already has an Agent Key from the Synapse Gateway Dashboard.

当开发者或 AI Agent 已经从 Synapse Gateway Dashboard 获取 Agent Key 时，使用这个示例。

```bash
pip install synapse-client
export SYNAPSE_ENV=staging
export SYNAPSE_API_KEY=agt_xxx
```

```python
from synapse_client import SynapseClient

# Use "staging" for testnet (free), "prod" for mainnet (real USDC).
# 使用 "staging" 连接测试网免费环境，使用 "prod" 连接主网真实 USDC 环境。
client = SynapseClient()

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

Full runbook: https://staging.synapse-network.ai/docs/sdk/python

完整接入手册：https://staging.synapse-network.ai/docs/sdk/python
