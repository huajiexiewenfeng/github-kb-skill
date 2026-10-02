# GitHub KB Skill

[English](README.md)

让 AI Agent 管理本地 GitHub 仓库收藏，并研究源码、issue、PR 和 release 的轻量 Skill。

把值得复用的仓库保存在本地，Agent 按当前问题查找已有源码、选择本地或远程证据，并在克隆成功后维护收藏索引。

## 能做什么

- 查找本地收藏的仓库和可复用代码。
- 通过 `gh` 或可用的 GitHub 工具读取 issue、PR、diff 和 release。
- 根据明确请求克隆仓库，成功后登记到 `CLAUDE.md`。
- 标明本地副本的版本，区分本地快照与远程最新状态。
- 保留已有仓库、索引内容和认证配置。

本项目提供 Agent 工作指令，不是可执行应用、向量数据库或搜索服务；不会自动同步仓库或为源码建立全文索引。

## 安装

将仓库克隆到尚未占用的目录：

```sh
git clone https://github.com/huajiexiewenfeng/github-kb-skill.git
```

把仓库内的 **`github-kb` 文件夹**复制到 Agent 的 Skill 目录，保持文件夹名为 `github-kb`。

| Agent | 用户级 Skill 目录 |
| --- | --- |
| Codex | `$CODEX_HOME/skills/github-kb`；未设置 `CODEX_HOME` 时使用 `~/.codex/skills/github-kb` |
| Claude Code | `~/.claude/skills/github-kb` |

已有同名 Skill 时先检查差异。其他 Agent 可按自身支持的 Skill 机制加载 `SKILL.md`；本次发布未验证各 Agent 的实际运行及自动发现行为。

使用 CLI 示例需安装 Git 和 [GitHub CLI](https://cli.github.com/)，需要账户权限的操作先完成 `gh` 登录。Agent 也可使用宿主提供的 GitHub 工具。

## 配置收藏目录

在当前请求或工作区指令中说明收藏根目录，也可以设置 Agent 环境变量 `GITHUB_KB_ROOT`。优先级为：当前请求 → 工作区指令 → 环境变量。未配置时，Agent 会建议 `~/github-kb`，并在首次写入前确认位置。

PowerShell 示例：

```powershell
$env:GITHUB_KB_ROOT = Join-Path $HOME 'github-kb'
```

在该终端中启动 Agent 才会继承此设置；已经运行的桌面应用不会自动获得新的环境变量。

索引位于 `<收藏根目录>/CLAUDE.md`，条目示例：

```markdown
- **cli** (`cli/cli`): GitHub 官方命令行工具
```

## 使用示例

```text
用 $github-kb 在我的收藏里找实现了 MCP server 的仓库。

用 $github-kb 查看 cli/cli 的最新 release，说明本次变化。

用 $github-kb 将 https://github.com/cli/cli 克隆到 ~/github-kb，并登记索引。

用 $github-kb 研究 owner/repo 的 PR 123，同时查看实际 diff。
```

当前项目开发直接使用项目上下文；远程研究不要求先查本地收藏。只读请求不改写索引，克隆失败不会登记成成功。

## 贡献

欢迎提交 issue 和 PR。修改聚焦收藏工作流、证据质量和实用的 Agent 指令，请勿提交私有收藏索引、凭据或个人机器路径。

## 许可证

[MIT](LICENSE) © 2026 huajiexiewenfeng。
