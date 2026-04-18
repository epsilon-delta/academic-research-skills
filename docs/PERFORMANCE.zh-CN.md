# ARS 性能说明

> **推荐模型：Claude Opus 4.6**，搭配 **Max plan**（或等效的 extended-thinking 配置）。
>
> 完整学术 pipeline（10 个阶段）会消耗**大量 token**。一次完整的端到端运行，输入可能超过 200K、输出超过 100K，具体取决于论文长度和修订轮次。请按预算使用。
>
> 单独运行某个 skill，例如只使用 `deep-research` 或 `academic-paper-reviewer`，成本会明显更低。

## 各模式 token 消耗估算

| Skill / 模式 | 输入 Token | 输出 Token | 估算费用（Opus 4.6） |
|---|---|---|---|
| `deep-research` socratic | ~30K | ~15K | ~$0.60 |
| `deep-research` full | ~60K | ~30K | ~$1.20 |
| `deep-research` systematic-review | ~100K | ~50K | ~$2.00 |
| `academic-paper` plan | ~40K | ~20K | ~$0.80 |
| `academic-paper` full | ~80K | ~50K | ~$1.80 |
| `academic-paper-reviewer` full | ~50K | ~30K | ~$1.10 |
| `academic-paper-reviewer` quick | ~15K | ~8K | ~$0.30 |
| **完整 pipeline（10 阶段）** | **~200K+** | **~100K+** | **~$4-6** |
| + 跨模型验证 | +~10K（外部） | +~5K（外部） | +~$0.60-1.10 |

*以上估算基于约 15,000 字论文和约 60 条参考文献。实际消耗会随着论文长度、修订轮次和对话深度变化。费用按 2026 年 4 月 Anthropic API 定价估算。*

## 推荐的 Claude Code 设置

| 设置 | 作用 | 如何启用 | 文档 |
|---|---|---|---|
| **Agent Team** | 启动 subagents 并行处理研究、写作和评审，是多 agent pipeline 的关键能力 | 设置 `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`（研究预览） | 实验性功能，暂无稳定文档 |
| **Ralph Loop** | 让长时间运行的 pipeline 阶段保持 session 活跃，避免 Claude 因超时中断 | 使用 `/ralph-loop` 启动 | 社区插件，实验性 |
| **Skip Permissions** | 跳过每次工具调用的确认弹窗，让整条 pipeline 可以连续执行 | 启动时使用 `claude --dangerously-skip-permissions` | [Permissions](https://docs.anthropic.com/en/docs/claude-code/cli-reference) · [Advanced Usage](https://docs.anthropic.com/en/docs/claude-code/advanced) |

> **⚠️ 关于 Skip Permissions：** 这个参数会禁用所有工具调用确认对话框。它对可信环境下的长时间 pipeline 很方便，但也会移除人工审批这层安全网。只有在你可以接受 Claude 自动执行文件读取、写入和 shell 命令时才建议启用。
