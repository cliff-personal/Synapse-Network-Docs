# Python First Call

Use this when the developer or AI agent already has an Agent Key from the Synapse Gateway Dashboard.

```bash
pip install synapse-client
export SYNAPSE_ENV=staging
export SYNAPSE_API_KEY=agt_xxx
```

```python
from synapse_client import SynapseClient

# Use "staging" for testnet (free), "prod" for mainnet (real USDC).
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
