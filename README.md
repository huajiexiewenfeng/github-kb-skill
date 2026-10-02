# GitHub KB Skill

[中文说明](README.zh-CN.md)

An agent skill for managing a local GitHub repository knowledge base, researching source code, issues, PRs, and releases.

Keep useful repositories in one local collection. Let your agent find existing source, choose local or remote evidence, and record successful clones without overwriting your index.

## What it does

- Finds repositories and reusable code in a local collection.
- Reads GitHub issues, pull requests, diffs, and releases with `gh` or available GitHub tools.
- Clones repositories when requested and records them in a `CLAUDE.md` index.
- Distinguishes local snapshots from current remote evidence.
- Preserves existing repositories, index entries, and authentication settings.

This repository contains instructions, not a search service, vector database, or executable application. It does not automatically sync repositories or index their contents.

## Install

Clone this repository into an unused directory:

```sh
git clone https://github.com/huajiexiewenfeng/github-kb-skill.git
```

Copy the **`github-kb` folder** into your agent's skill directory. Keep its name `github-kb`.

| Agent | User skill directory |
| --- | --- |
| Codex | `$CODEX_HOME/skills/github-kb`, or `~/.codex/skills/github-kb` when `CODEX_HOME` is unset |
| Claude Code | `~/.claude/skills/github-kb` |

If a skill already exists there, review it before replacing it. Other agents can use the `SKILL.md` instructions if their skill mechanism supports this format. Host compatibility and automatic discovery depend on the agent; cross-agent runtime behavior has not been tested in this release.

For CLI examples, install Git and [GitHub CLI](https://cli.github.com/) and authenticate `gh` for operations that need account access. The instructions also allow available GitHub tools instead of `gh`.

## Configure your collection

Tell the agent your collection root in the request or workspace instructions, or set `GITHUB_KB_ROOT` in the agent's environment. Resolution order is: current request → workspace instructions → environment variable. Without a configured root, the agent suggests `~/github-kb` and confirms it before a first write.

For example, on PowerShell:

```powershell
$env:GITHUB_KB_ROOT = Join-Path $HOME 'github-kb'
```

Set this before launching your agent from that shell. Already running desktop applications will not inherit the changed environment.

The collection index is `<collection-root>/CLAUDE.md`. A minimal entry looks like:

```markdown
- **cli** (`cli/cli`): GitHub's command-line interface
```

## Example requests

```text
Use $github-kb to find a repository in my collection that implements an MCP server.

Use $github-kb to research cli/cli's latest release and explain the changes.

Use $github-kb to clone https://github.com/cli/cli into my collection at ~/github-kb
and add it to the index.

Use $github-kb to inspect PR 123 in owner/repo, including the actual diff.
```

The skill skips the global collection for ordinary work in a known current project. Remote research does not require a local collection, and read-only requests do not rewrite the index.

## Contribute

Issues and pull requests are welcome. Keep changes focused on repository collection workflows, evidence quality, and practical agent instructions. Do not include private collection indexes, credentials, or personal machine paths.

## License

[MIT](LICENSE) © 2026 huajiexiewenfeng.
