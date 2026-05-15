# Credentials

Canonical credentials docs:

https://docs.synapse-network.ai/concepts/budget-isolation

Agent runtime rule:

- Use an `agt_xxx` Agent Key with `SynapseClient`.
- Do not give agents owner private keys, wallet mnemonics, or owner JWTs.
- Use owner/admin setup only when the user explicitly asks to issue or manage credentials.
