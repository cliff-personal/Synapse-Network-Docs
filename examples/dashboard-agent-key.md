# Get an Agent Key

The fastest onboarding path is dashboard-issued credentials.

最快接入路径是通过 Dashboard 签发凭据。

1. Open the Synapse Dashboard: https://www.synapse-network.ai
2. Connect wallet as the owner.
3. Generate an Agent Key.
4. Copy the key that starts with `agt_`.
5. Give only that Agent Key to the agent runtime.

1. 打开 Synapse Dashboard：https://www.synapse-network.ai
2. 以 owner 身份连接钱包。
3. 生成 Agent Key。
4. 复制以 `agt_` 开头的 key。
5. 只把这个 Agent Key 交给 Agent 运行时。

The agent runtime should not receive owner private keys, wallet mnemonics, or owner JWTs.

Agent 运行时不应该接收 owner 私钥、钱包助记词或 owner JWT。

Full docs: https://docs.synapse-network.ai/concepts/budget-isolation

完整文档：https://docs.synapse-network.ai/concepts/budget-isolation
