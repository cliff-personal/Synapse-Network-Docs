# AGENTS.md

Read `llms.txt` first.

This repository is intentionally small. Keep it as a GitHub discovery funnel, agent-readable index, and public-source mirror for docs pages that expose `Open in GitHub`.

本仓库刻意保持轻量。它是 GitHub 发现入口和 Agent 可读索引，不是完整产品文档站的副本。

README language layout:

- English default: `README.md`
- Simplified Chinese: `README.zh-CN.md`
- Do not interleave English and Chinese in the same README body.

README 语言结构：

- 英文默认页：`README.md`
- 简体中文页：`README.zh-CN.md`
- 不要在同一个 README 正文中交替混排中英文。

Rules:

1. Keep README focused on TTFC, positioning, and links to staging docs.
2. Keep `llm-instructions.md` optimized for coding agents.
3. Public source-view links may point here, but do not add "Edit this page" flows until rendered docs are generated from this repo.
4. Do not include real credentials, private keys, JWTs, provider secrets, or production logs.
5. Do not use the old `gateway` on `synapse.network` domain; the staging docs domain is `staging.synapse-network.ai`.
6. Product name is SynapseNetwork. Do not use old agent-payment brand labels as the product name.
7. Describe the product as a platform where agents call APIs and make small USDC payments through blockchain-backed settlement.
8. Keep language switchers at the top of localized README files.
9. `content/docs/**` is a one-way public mirror from the private `Synapse-Network/services/docs-front/content/docs/**` tree. Do not hand-edit mirrored docs pages unless the mirror contract changes.

规则：

1. README 聚焦 TTFC、定位和 staging docs 链接。
2. `llm-instructions.md` 优先服务编码 Agent。
3. 在 docs-site 页面由本仓库生成之前，不要添加 "Edit this page"。
4. 不要包含真实凭据、私钥、JWT、provider secret 或生产日志。
5. 不要使用旧 `synapse.network` gateway 域名；staging docs 域名是 `staging.synapse-network.ai`。
6. 产品名是 SynapseNetwork，不要把旧的 agent-payment 命名当作产品名。
7. 产品描述应表达：Agent 通过平台调用接口，并通过区块链支持的 USDC 结算完成小额付款。
8. 在本地化 README 顶部保留语言切换链接。
