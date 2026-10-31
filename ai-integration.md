# AI-READONLY: 跨 AI 接入与同步规范

## 1. 统一读取原则
Markdown 是跨平台中立格式。AI 平台需获得 GitHub 授权或访问公开仓库的权限。公开仓库可匿名读取；私有仓库需 OAuth、GitHub App 或细粒度 PAT。

推荐读取顺序：README.md、identity/profile.md、workflow/preferences.md，再按任务读取相关目录。不要无差别注入整个仓库。

## 2. 平台接入
- **ChatGPT：** 通过支持 GitHub 的连接器/应用或自建 MCP 服务读取。写入能力取决于连接器权限，读取权限不等于写入权限。
- **Gemini：** 通过 Gemini API/自建应用读取 GitHub REST API 或 raw Markdown。Token 存在服务端 Secret Manager。
- **Claude：** 通过 GitHub 集成（若账户/产品可用）或自建 MCP Server 读取；写操作需显式确认。
- **Meta Muse / OpenAI Dots / 其他 Agent：** GitHub 连接、定时同步和写入能力取决于产品当前开放能力与账户权限。先验证连接器能力，不假设自动支持。

## 3. GitHub API 读取示例
```bash
curl -L https://raw.githubusercontent.com/sxsxsx3456/personal-ai-archive/main/workflow/preferences.md
curl -L https://api.github.com/repos/sxsxsx3456/personal-ai-archive/contents/workflow/preferences.md
```
私有仓库需使用授权令牌；不要硬编码或提交 Token。

## 4. 自动更新协议
1. 任务完成后判断是否产生长期有效的新事实、偏好、决策或经验。
2. 生成候选更新，包含目标文件、理由、来源、日期和 Markdown diff。
3. 检查敏感信息、客户机密、未经证实的推断和重复内容。
4. 本人批准后，通过独立写入身份创建分支/提交或 Pull Request。
5. 合并后记录提交 SHA；错误时使用 Git revert 回退。

严禁自动覆盖整份档案、将临时指令提升为长期偏好、将推断写成事实、提交凭据或绕过默认分支保护。

## 5. 权限模型
- 日常读取：只读权限。
- 更新：独立 GitHub App 或 fine-grained PAT，仅授予目标仓库所需 Contents 与 Pull requests 权限。
- 不授予不必要的 Administration 权限；Token 放入密钥管理服务，设置过期并轮换。

## 6. 同步频率
按需读取；任务结束时仅提出长期有效信息的候选写入；每月人工审查重复、过期和冲突内容。
