# ARS 安装设置

Academic Research Skills 的前置需求与可选设置。若你只需要 Markdown 输出和默认的 Claude Opus 4.6 pipeline，大部分内容都可以跳过，先看下方“最小可行设置”即可。

---

## 最小可行设置

1. 安装 Claude Code（见下方）。
2. 设置 `ANTHROPIC_API_KEY`。
3. 在这个仓库里，或任何把 ARS 放在 `.claude/skills/` 下的项目里运行 `claude`。

这样就足够得到 Markdown 输出和 DOCX 转换说明。本文其余部分都是可选增强。

---

## 安装 Claude Code

**推荐：原生安装器**（不需要 Node.js，支持自动更新）：

```bash
# macOS / Linux
curl -fsSL https://claude.ai/install.sh | bash

# Windows（PowerShell）
irm https://claude.ai/install.ps1 | iex
```

<details>
<summary>备选方案：npm 安装（已弃用）</summary>

需要 Node.js 18+。

```bash
npm install -g @anthropic-ai/claude-code
```

</details>

## 设置 API Key

你需要一个 Anthropic API key，可在 <https://console.anthropic.com/> 获取。

```bash
# Claude Code 首次运行时会提示输入 API key
claude
```

也可以直接设置环境变量：

```bash
export ANTHROPIC_API_KEY=sk-ant-xxxxx
```

## DOCX 输出（可选）

如果要直接生成 `.docx`，需要安装 [Pandoc](https://pandoc.org/)。如果系统里没有 Pandoc，formatter 会退回为 Markdown 输出加 DOCX 转换说明。

```bash
# macOS
brew install pandoc

# Linux (Debian/Ubuntu)
sudo apt-get install pandoc

# Windows — 请从 https://pandoc.org/installing.html 下载
```

## LaTeX / PDF 输出（可选）

PDF 输出需要 [tectonic](https://tectonic-typesetting.github.io/) 和指定字体。**这是可选项**，没有这些依然可以使用 Markdown 输出和 DOCX 转换说明。

```bash
# macOS
brew install tectonic

# Linux (Debian/Ubuntu)
curl --proto '=https' --tlsv1.2 -fsSL https://drop-sh.fullyjustified.net | sh

# Windows — 请从 https://tectonic-typesetting.github.io/en-US/install.html 下载
```

**所需字体**（用于 APA 7.0 中文输出）：

- **Times New Roman**：macOS/Windows 通常已预装；Linux 可安装 `ttf-mscorefonts-installer`
- **Source Han Serif TC VF**（思源宋体）— 从 [Google Fonts](https://fonts.google.com/specimen/Noto+Serif+TC) 或 [Adobe GitHub](https://github.com/adobe-fonts/source-han-serif) 下载
- **Courier New**：通常已预装

> 如果你只需要 Markdown 输出或 DOCX 转换说明，可以完全跳过这一步。直接生成 `.docx` 需要 Pandoc，生成 PDF 需要 `tectonic`。

---

## 跨模型验证（可选）

ARS 只用 Claude Opus 4.6 也能完整运行。如果你想提高置信度，可以额外启用第二个 AI 模型，独立执行完整性验证并挑战 devil's advocate。

### 快速设置

```bash
# 设置 API key（可二选一，也可都设置）
export OPENAI_API_KEY="sk-your-key-here"         # GPT-5.4 Pro
export GOOGLE_AI_API_KEY="AIza-your-key-here"   # Gemini 3.1 Pro

# 选择跨验证模型
export ARS_CROSS_MODEL="gpt-5.4-pro"
# 或：export ARS_CROSS_MODEL="gemini-3.1-pro-preview"

# 像平常一样运行 Claude Code，跨验证会自动启用
claude
```

### 启用后的差异

| 功能 | 未启用 | 启用后 |
|---|---|---|
| 完整性验证 | 单模型 100% 检查 | + 30% 样本由第二模型独立验证 |
| Devil's Advocate | 单模型 DA | + 跨模型生成独立 critique，并加入新的发现 |
| 同行评审 | 5 位 reviewer（同模型） | 同样的 5 位 reviewer，另加跨模型 DA critique / calibration 支持 |

### 成本

完整 pipeline 大约会额外增加 ~$0.60-1.10 的跨模型 API 成本（按 GPT-5.4 Pro 定价估算）。详细拆解见 [`shared/cross_model_verification.md`](../shared/cross_model_verification.md)。

### 没有 API key 也没关系

如果没有设置 `ARS_CROSS_MODEL`，系统会和以前完全一样运行，不会额外增加任何开销。

---

## 安装方式

### 方法一：作为项目 Skills（推荐）

把仓库 clone 到项目的 `.claude/skills/` 目录：

```bash
cd /path/to/your/project
mkdir -p .claude/skills
git clone https://github.com/Imbad0202/academic-research-skills.git .claude/skills/academic-research-skills
```

然后把 `.claude/CLAUDE.md` 的内容复制到你项目的 `.claude/CLAUDE.md` 中；如果原来就有，就做合并。

> **全局安装：** 如果你希望所有项目都能使用这些 skills，可以安装到 `~/.claude/skills/`：
>
> ```bash
> mkdir -p ~/.claude/skills
> git clone https://github.com/Imbad0202/academic-research-skills.git ~/.claude/skills/academic-research-skills
> ```

### 方法二：作为独立项目使用

```bash
git clone https://github.com/Imbad0202/academic-research-skills.git
cd academic-research-skills
claude
```

<details>
<summary><strong>没有 Git？也可以直接下载 ZIP</strong></summary>

1. 访问 <https://github.com/Imbad0202/academic-research-skills>
2. 点击绿色 **Code** 按钮 → **Download ZIP**
3. 解压到你想放置的位置
4. 若按方法一使用：把解压后的文件夹移动到项目里的 `.claude/skills/academic-research-skills`
5. 若独立使用：在解压后的目录打开终端，运行 `claude`

</details>

### 方法三：在 Claude Cowork（桌面版）中使用

你可以在 [Claude Cowork](https://claude.com/product/cowork) 中使用这些 skills，它是 Claude Desktop 的 agentic workspace。

**选项 A：文件夹访问（最快）**

1. 先把仓库 clone 到本地：
   ```bash
   git clone https://github.com/Imbad0202/academic-research-skills.git ~/academic-research-skills
   ```
2. 打开 Claude Desktop，点击顶部的 **Cowork** 标签
3. 选择本地 `academic-research-skills` 文件夹作为工作目录
4. Claude 会从各个 `SKILL.md` 自动识别并按需加载 skills

**选项 B：作为项目 Skills**

如果你已经在 Cowork 中有项目目录：

```bash
cd /path/to/your/project
mkdir -p .claude/skills
git clone https://github.com/Imbad0202/academic-research-skills.git .claude/skills/academic-research-skills
```

相关 skills 会在需要时自动加载，例如说“帮我写论文”会触发 `academic-paper`。

**要求：** Claude Desktop（最新版）且已启用 Cowork；付费套餐（Pro、Max、Team 或 Enterprise）。

### 方法四：配合 claude.ai（网页版）使用

你也可以通过 [claude.ai](https://claude.ai) 的 **Project** 功能结合 GitHub 集成来使用这些 skills，不需要安装 Claude Code。

1. 登录 [claude.ai](https://claude.ai)（需要付费套餐）
2. 新建一个 Project：**Projects** → **Create Project**
3. 从 GitHub 导入：在 Project 中点击 **Files** → **+** → **GitHub** → 选择 `Imbad0202/academic-research-skills`

   **推荐勾选项**（避免超出容量）：

   | 选择 | 目录 | 原因 |
   |---|---|---|
   | ✅ | `.claude/` | 路由规则 |
   | ✅ | `deep-research/` | 核心 skill |
   | ✅ | `academic-paper/` | 核心 skill |
   | ✅ | `academic-paper-reviewer/` | 核心 skill |
   | ✅ | `academic-pipeline/` | 核心 skill |
   | ✅ | `shared/` | 跨模型验证、handoff schema |
   | ✅ | `MODE_REGISTRY.md` | mode 定义 |
   | ❌ | `examples/` | 大约占 39% 容量，空间紧张时可跳过 |
   | ❌ | `.github/`、README、LICENSE 等 | 对功能运行不是必需的 |

4. （可选）把 `.claude/CLAUDE.md` 的内容填进 Project 的 **Instructions**，可获得更好的路由效果
