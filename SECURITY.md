# AI-READONLY: 安全与版本保护策略

## 公开仓库数据分级
**允许：** 经本人确认的公开职业摘要、通用偏好、技能清单、非敏感项目总结。

**禁止：** 密码、API Key、PAT、个人证件号码、私人地址/电话、健康与财务隐私、客户资料、合同/报价、公司内部流程细节、未公开商业信息、私人聊天原文。

## 分支保护建议
在 GitHub Settings 为默认分支配置 Ruleset / Branch protection：
- Require a pull request before merging。
- Require at least 1 approval（个人仓库可由本人审查 PR）。
- Require conversation resolution。
- Block force pushes。
- Restrict deletions。
- 不允许 Agent 直接推送默认分支。

规则可用性取决于仓库计划、可见性和 GitHub 当前策略；配置后需核实是否生效。

## 版本回退
优先使用 `git revert <commit>` 创建反向提交，保留审计历史。恢复单个文件时从指定历史版本取回内容，再通过新提交恢复。避免随意 force push。
