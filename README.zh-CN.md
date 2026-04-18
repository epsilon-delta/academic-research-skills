# Academic Research Skills for Claude Code

[![Version](https://img.shields.io/badge/version-v3.3.6-blue)](https://github.com/Imbad0202/academic-research-skills/releases/tag/v3.3.6)
[![License: CC BY-NC 4.0](https://img.shields.io/badge/license-CC%20BY--NC%204.0-lightgrey)](https://creativecommons.org/licenses/by-nc/4.0/)
[![Sponsor](https://img.shields.io/badge/sponsor-Buy%20Me%20a%20Coffee-orange?logo=buy-me-a-coffee)](https://buymeacoffee.com/crucify020v)

[English](README.md) | [繁体中文版](README.zh-TW.md)

一套面向学术研究场景的 Claude Code 技能集合，覆盖从研究到论文发表的完整流程。

> **AI 是你的副驾驶，不是机长。** 这套工具不会替你写论文。它负责那些最耗时但适合辅助处理的工作，比如检索文献、整理引用、核对数据、检查逻辑一致性，让你把精力放在真正需要研究者判断的部分：定义问题、选择方法、解释结果，以及写出你的核心论点。
>
> 它也不是为了帮你掩盖使用 AI 的事实。它的目标是帮助你写得更好。Style Calibration 会学习你过去作品的表达习惯，Writing Quality Check 会标出常见的 AI 痕迹式表达。目标是提升质量，而不是规避披露。

## 项目是什么

ARS（Academic Research Skills）是一套给 Claude Code 使用的学术研究技能库，核心由 4 个部分组成：

- `deep-research`：研究问题澄清、文献检索、事实核查、系统综述、Socratic 引导式研究
- `academic-paper`：论文提纲、论证、正文、摘要、引用格式与导出
- `academic-paper-reviewer`：多视角模拟审稿与复审
- `academic-pipeline`：把研究、写作、评审、修订串成一个完整流程

完整架构见 [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)。

## 设计原则

- 人始终在环：关键阶段必须由用户确认，尤其是提纲、评审决策和完整性闸门
- 辅助而非代写：工具帮助研究者工作，不替代研究判断
- 暴露失败模式：通过完整性检查与 reviewer calibration，让模型的盲点可见，而不是假装“全都正确”

## 快速开始

1. 安装 Claude Code，并把本仓库放进技能目录
2. 启动 `claude`
3. 用自然语言描述目标，系统会自动匹配合适的 skill 和 mode

示例：

```text
我想完整做一篇关于生成式 AI 如何影响高校学习成效评估的研究论文
```

```text
引导我研究少子化对民办高校治理的影响
```

```text
帮我评审这篇论文
```

更详细的安装步骤见 [QUICKSTART.md](QUICKSTART.md) 和 [docs/SETUP.zh-CN.md](docs/SETUP.zh-CN.md)。

## 完整流程长什么样

完整 pipeline 的主线如下：

1. `RESEARCH`：明确研究问题、方法和核心文献
2. `WRITE`：生成论文配置、提纲和正文
3. `2.5 INTEGRITY`：第一次完整性核查
4. `REVIEW`：多 reviewer 模拟审稿
5. `REVISE`：根据意见修订
6. `RE-REVIEW` / `RE-REVISE`：验证修订是否到位
7. `4.5 FINAL INTEGRITY`：最终完整性核查
8. `FINALIZE`：导出 Markdown / DOCX / LaTeX / PDF
9. `PROCESS SUMMARY`：生成研究协作过程记录

这一流程的详细阶段说明见 [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)。

## 常见用法

### 1. 做前期研究

```text
研究 AI 对高校质量保障的影响
```

### 2. 用引导模式收敛研究问题

```text
我还没想清楚研究问题，帮我一步步梳理
```

### 3. 从头写论文

```text
帮我写一篇关于人口下降对地方高校管理策略影响的论文
```

### 4. 评审已有论文

```text
评审这篇论文
```

### 5. 跑完整流程

```text
我想做一篇完整研究论文，从选题、写作到评审修订都一起推进
```

## 支持的语言与格式

- 英文
- 中文
- 双语摘要（中文 + 英文）
- APA 7.0、Chicago、MLA、IEEE、Vancouver 引用格式

说明：

- 仓库原生文档以英文和繁体中文为主
- 当前分支正在补充简体中文适配
- 某些 `SKILL.md` 中的触发关键词现在同时包含繁体和简体表达

## 重要入口

- [README.md](README.md)：英文主文档
- [README.zh-TW.md](README.zh-TW.md)：繁体中文文档
- [docs/SETUP.zh-CN.md](docs/SETUP.zh-CN.md)：简体中文安装说明
- [docs/PERFORMANCE.zh-CN.md](docs/PERFORMANCE.zh-CN.md)：简体中文性能与成本说明
- [QUICKSTART.md](QUICKSTART.md)：快速开始
- [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)：完整架构
- [examples/showcase/](examples/showcase/)：完整流水线的实际产物

## 许可

本项目使用 [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) 许可，仅限非商业用途。
