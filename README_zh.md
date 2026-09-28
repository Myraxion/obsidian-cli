<div align="center">

# obsidian-cli

适用于 [Obsidian 官方桌面 CLI](https://obsidian.md/help/cli) 的 Agent Skill。

[![Skills](https://img.shields.io/badge/skills.sh-Myraxion%2Fobsidian--cli-purple?style=flat-square)](https://skills.sh/)
[![Obsidian](https://img.shields.io/badge/Obsidian-1.12.7%2B-705dcf?style=flat-square&logo=obsidian&logoColor=white)](https://obsidian.md/)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](LICENSE)

[English](README.md) | [简体中文](README_zh.md)

</div>

---

将 AI Coding Agent（Claude Code、Antigravity、OpenHands 等）与 Obsidian 官方桌面 CLI 深度连接。支持实时全文检索、双链安全重构、元数据属性更新、日记流记录、待办任务聚合、Bases 数据库管理、工作区切换与本地历史版本恢复。

## 特性

- **面向用户**：专注于日常知识管理、双链关系与任务聚合。剔除了其他选择中常见的开发者调试命令（`eval`、DOM 探测、调试器控制），减少上下文噪音并避免 Agent 产生误调用。
- **实用的工具分工**：避免像其他选择那样强制通过 CLI 参数创建多行笔记（极易遭遇 Shell 引号转义与截断问题）。由原生文件工具处理笔记内容，CLI 仅负责 Obsidian 的核心能力（双链安全重命名/移动、标签页控制与内存索引检索）。
- **极低的上下文占用**：入口仅约 1.7 KB，各领域指南按需加载；避免了其他选择一次性向 Prompt 注入 20–30+ KB 全量手册带来的 Token 浪费。
- **Agent 会话稳定性**：明确防范自毁性操作（如重启窗口或禁用宿主插件），确保 Agent 在作为 Obsidian 内部插件运行时能够安全稳定工作。
- **对齐最新官方规范（v1.12.7+）**：紧跟官方最新桌面 CLI 行为，剔除早期预览版本残留的临时 Workaround 与冗余参数。
- **遵循 KISS 原则**：摒弃繁琐的启动探测脚本与循环检查逻辑，降低执行开销与跨平台环境摩擦。

## 环境准备

1. **Obsidian 1.12.7 或更高版本**：从 [obsidian.md/download](https://obsidian.md/download) 下载并安装桌面应用安装包（仅在应用内检查更新可能不会升级底层安装包版本）。
2. **启用 CLI**：在 Obsidian 中开启 **设置 → 常规 → 命令行界面**，并允许系统管理员注册提示。
3. **验证连通性**：保持 Obsidian 桌面端运行，在终端中验证：

   ```sh
   obsidian version
   obsidian vault info=path
   ```

## 安装指南

### 使用 skills CLI（推荐）

```sh
npx skills add Myraxion/obsidian-cli
```

### 手动安装

将 `skills/obsidian-cli/` 目录复制到对应 Agent 的技能目录中：

- 项目级：`.agents/skills/obsidian-cli/`（或 `.claude/skills/obsidian-cli/`）
- 全局级：`~/.agents/skills/obsidian-cli/`（或 `~/.claude/skills/obsidian-cli/`）

## 文档结构

本技能采用按需加载模式以保持基础上下文占用最小：

| 文件 | 覆盖范围 |
|------|---------|
| [`skills/obsidian-cli/SKILL.md`](skills/obsidian-cli/SKILL.md) | 安全红线规则与任务路由逻辑 |
| [`skills/obsidian-cli/references/note-operations.md`](skills/obsidian-cli/references/note-operations.md) | 笔记读写、模板实例化、双链安全重命名/移动、日记与本地历史快照 |
| [`skills/obsidian-cli/references/search-indexes.md`](skills/obsidian-cli/references/search-indexes.md) | 全文检索、Bases 数据库、Frontmatter 属性、标签、双链与待办任务 |
| [`skills/obsidian-cli/references/app-commands.md`](skills/obsidian-cli/references/app-commands.md) | 命令面板命令发现与执行 |
| [`skills/obsidian-cli/references/workspace-vault.md`](skills/obsidian-cli/references/workspace-vault.md) | 工作区布局、标签页、插件主题生态、多 Vault 定位与 Sync |

## 故障排查

有关常见问题的排查说明，请参阅[官方 CLI 排查指南](https://obsidian.md/help/cli#Troubleshooting)。

- **Windows**：若直接运行 `obsidian` 弹出 GUI 窗口或终端无输出挂起，请调用注册的终端重定向器 `Obsidian.com` 而非 `Obsidian.exe`。
- **macOS**：注册会将 `/usr/local/bin/obsidian` 软链接到程序。请确保 `/usr/local/bin` 已包含在系统的 `PATH` 中。
- **Linux**：二进制文件位于 `~/.local/bin/obsidian`。请确保 `~/.local/bin` 已包含在系统的 `PATH` 中。
- **软件更新后注册失效**：若 Obsidian 更新后 CLI 无法调用，在 **设置 → 常规** 中将命令行开关先关闭再重新开启，并重启终端即可。

## 开源许可

本项目基于 [MIT 许可证](LICENSE) 开源。
