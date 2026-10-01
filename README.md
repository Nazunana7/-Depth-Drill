# Depth Drill｜向下探索训练器

**一个导师型 Skill,训练"向下探索能力",而不是增加知识量。**
A Socratic depth-training skill that moves from working answers to mechanisms, assumptions, boundaries, verification, and transfer.

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Type](https://img.shields.io/badge/type-skills--only%20plugin-2563EB.svg)](#仓库结构)
[![Platform](https://img.shields.io/badge/platform-Codex%20%7C%20ChatGPT-000000.svg)](#在-codex-中安装)

它会根据当前对话自动判断是否启动,也可以在需要时手动调用。目标路径:

```text
理解 → 机制 → 假设 → 验证 → 边界 → 例外 → 优化 → 迁移 → 新问题
```

---

## 启动方式

| 方式 | 触发 |
|------|------|
| 自动触发 | 当对话明确要求被追问、验证理解或继续向下探索时 |
| 快捷触发 | 输入 `\dd 你的主题` |
| 单独触发 | 输入 `\dd`,技能会先询问当前进展 |
| Codex 原生显式调用 | `$depth-drill` |

## 它如何工作

- 每次只推进一个最关键的问题。
- 用户没有明确要求时,不直接提供下一层答案。
- 根据回答动态选择机制、假设、边界、验证、应用或迁移。
- 明确区分"能复述"和"能预测、处理反例、迁移应用"。
- 有明确停止条件,避免为了深度而无限追问。

## 仓库结构

```text
.
├── .agents/plugins/marketplace.json
└── plugins/
    └── depth-drill/
        ├── .codex-plugin/plugin.json
        └── skills/
            └── depth-drill/
                ├── SKILL.md
                └── agents/openai.yaml
```

这是 skills-only Plugin:不需要 MCP Server,也不需要外部认证。

## 在 Codex 中安装

在 Codex 中添加 marketplace:

```bash
codex plugin marketplace add Nazunana7/depth-drill
```

再打开 `/plugins`,找到 **Depth Drill** 并安装。也可以固定分支:

```bash
codex plugin marketplace add Nazunana7/depth-drill --ref main
```

> 本仓库原名 `-Depth-Drill`,已改名为 `depth-drill`。GitHub 会自动把旧地址重定向到新地址,所以旧的 clone / install 命令仍然可用,但建议改用上面的新写法。

如果只想把它作为普通本地 Skill 使用,也可以把下面的目录复制到 Codex 用户的 Skill 目录:

```bash
mkdir -p ~/.agents/skills
cp -R plugins/depth-drill/skills/depth-drill ~/.agents/skills/depth-drill
```

## 在网页版 ChatGPT 中使用

普通 standalone Skill 不能直接用于网页版 ChatGPT。这个仓库已经按 Plugin 形式打包,因此可以选择以下路径:

### 公开 Plugin

将 skills-only Plugin 提交到 OpenAI Plugin submission portal,通过审核并发布后,它会进入 ChatGPT 与 Codex 共用的 universal Plugins Directory。

公开提交通常需要:

- Platform 组织中的 **Apps Management: Write** 权限。
- 已验证的个人开发者或企业身份。
- 网站、支持地址、隐私政策和条款页面。
- 至少 5 个正面测试用例和 3 个负面测试用例。
- 最终 Skill bundle 和插件 listing 信息。

### 工作区 Plugin

如果使用 ChatGPT Business、Enterprise 或 Edu workspace,管理员可以:

1. 打开 **Admin → Plugins**。
2. 选择 **Add → Import marketplace**。
3. 填入 GitHub 仓库 URL。
4. 同步后,工作区成员可以从 Plugins Directory 安装。

### 个人 Plugin

ChatGPT 的 Personal Plugins 区域会显示个人 marketplace 中可用的插件;当前官方 Web 个人插件 quickstart 主要以 MCP-backed personal plugin 为例。对于 skills-only Plugin,最明确的网页版路径是工作区 marketplace 导入或公开提交审核。

## 更新 Skill

编辑:

```text
plugins/depth-drill/skills/depth-drill/SKILL.md
```

同时检查:

```text
plugins/depth-drill/skills/depth-drill/agents/openai.yaml
plugins/depth-drill/.codex-plugin/plugin.json
```

修改后重新测试自动触发和 `\dd` 手动触发,再更新 plugin `version`。

## License

[MIT](LICENSE)
