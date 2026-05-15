# GitHub Growth Checklist

Use GitHub as the top-of-funnel surface and the production docs site as the conversion surface.

把 GitHub 作为漏斗顶层入口，把 production docs 站点作为最终转化阵地。

English appears first. Chinese follows each major section.

英文在前，中文说明紧随其后。

## Repository About

仓库 About 区域。

Recommended description:

SynapseNetwork: AI agents call APIs and make small USDC payments through blockchain-backed settlement.

推荐描述：

SynapseNetwork：AI Agent 通过平台调用 API，并通过区块链支持的 USDC 结算完成小额付款。

Recommended website:

https://docs.synapse-network.ai/

Primary dashboard CTA:

https://www.synapse-network.ai

Recommended topics:

- ai-agents
- crypto-payments
- usdc
- smart-contracts
- agent-framework
- web3-gateway
- agent-payments
- api-gateway
- developer-tools

推荐 topics：

- ai-agents
- crypto-payments
- usdc
- smart-contracts
- agent-framework
- web3-gateway
- agent-payments
- api-gateway
- developer-tools

## Environment Message

Keep the README clear that:

- `staging` is live now, testnet-backed, and uses MockUSDC.
- `prod` uses the production docs and app domain and real USDC when production access is enabled.
- If live production docs health checks fail, report it as a release blocker instead of switching the GitHub funnel back to staging.

环境信息必须明确：

- `staging` 当前可用，基于测试网，使用 MockUSDC。
- `prod` 使用 production docs/app 域名，并在 production access 开放时使用真实 USDC。
- 如果线上 production docs health check 失败，应作为 release blocker 记录，不要把 GitHub funnel 切回 staging。

## Brand Message

Use SynapseNetwork as the product name.

Do not use old agent-payment labels as the product name. "Agent payments" can be used as a category or capability, not as the product brand.

品牌信息：

产品名使用 SynapseNetwork。

不要把旧的 agent-payment 命名当作产品名。"Agent payments" 可以作为能力类别描述，但不是产品品牌。

## V1 Contribution Loop

Use these calls to action:

- Report docs issue
- Ask in Community / Discussions
- Open SDK issue

Do not use "Edit this page" until docs-site pages are generated from this repository. That prevents users from editing a short GitHub stub that does not match the polished docs page they just read.

V1 使用这些行动入口：

- Report docs issue
- Ask in Community / Discussions
- Open SDK issue

在 docs-site 页面由本仓库生成之前，不要使用 "Edit this page"。这样可以避免用户从精美 docs 页面跳到不匹配的 GitHub 简略 stub。
