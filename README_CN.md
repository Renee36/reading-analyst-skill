# 阅读分析师 Skill

[![适用于 Claude Code](https://img.shields.io/badge/适用于-Claude%20Code-blueviolet?logo=anthropic)](https://claude.ai/claude-code)
[![适用于任何 LLM](https://img.shields.io/badge/同样适用于-任何%20LLM-green)](#方式二任何-ai-工具)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**将多年阅读记录转化为十章结构化个人阅读智能报告。**

[English README](README.md)

---

## 与同类产品的区别

| 功能 | 阅读分析师 Skill | Smart Reading Tracker | CastReader | 通用读书报告 |
|------|-----------------|----------------------|------------|-------------|
| 十章结构化分析 | :white_check_mark: | :x: | :x: | :x: |
| 30 维度知识雷达图 | :white_check_mark: | :x: | :x: | :x: |
| 双书单推荐（填空白 + 深耕热爱） | :white_check_mark: | :x: | :x: | :x: |
| 品味画像 + 人物关键词 | :white_check_mark: | :x: | :x: | :x: |
| 阅读开创价值分析 | :white_check_mark: | :x: | :x: | :x: |
| 离线 / 本地运行 | :white_check_mark: | 视情况 | :x: | 视情况 |
| 多年阅读演化脉络 | :white_check_mark: | :x: | :x: | :x: |
| 最低输入：仅书名 | :white_check_mark: | 需要 ISBN | 需要 ISBN | 不一定 |

## 核心能力

- **品味画像** —— 用人物刻画关键词提炼你的阅读人格（如 `方法论控` `科学审美` `长期主义`）
- **30 维度知识雷达** —— 基于 UNESCO + 中图法框架，将你的阅读映射到人类知识全版图
- **双书单推荐** —— 书单 A 填补知识空白；书单 B 深耕你的热爱领域
- **演化脉络** —— 追溯多年阅读兴趣的迁移路径
- **有趣的洞察** —— 发现隐藏模式：执念书单、文化暗线、数量跃迁
- **开创价值分析** —— 揭示你的阅读积累能创造什么独特价值

## 报告内容：十章概览

| 章节 | 标题 | 内容 |
|------|------|------|
| 1 | 总览数据 | 时间跨度、总量、年度走势柱状图 |
| 2 | 品类分布 | 按数量降序排列，含占比 |
| 3 | 品味画像 | 一句话人格 + 人物关键词 + 带证据的品味特征 |
| 4 | 高分书目 | 15-25 本最高评分书目 + 模式分析 |
| 5 | 演化脉络 | 3-6 个阅读阶段、转折点、预测 |
| 6 | 知识网络 | 8 大领域 × 30 维度、雷达图、缺陷分析 |
| 7 | 书单推荐 | 10 本填补空白 + 10 本深耕热爱 |
| 8 | 有趣的洞察 | 5-7 个数据隐藏发现 |
| 9 | 开创价值 | 独特知识组合 + 输出方向 |
| 10 | 附录 | 按年份完整书目清单（可选） |

## 输入要求

你可以**仅凭书名**开始——提供的数据越多，报告越丰富。

### 输入层级

| 输入层级 | 你提供什么 | 可生成章节 | 覆盖率 |
|---------|-----------|-----------|--------|
| **最低门槛** | 仅书名 | Ch1（部分）、Ch2、Ch3（基础版）、Ch6、Ch7、Ch9 | ~6/10 |
| **建议输入** | 书名 + 阅读年份 | + Ch1（完整）、Ch5（演化脉络）、Ch8（洞察） | ~8/10 |
| **完整输入** | 书名 + 年份 + 评分 + 分类 | 全部 10 章，完整深度 | 10/10 |

### 各章节与输入数据的对应关系

| 章节 | 仅书名 | + 年份 | + 评分 | + 分类 |
|------|:------:|:------:|:------:|:------:|
| 1. 总览数据 | 部分 | :white_check_mark: 完整 | :white_check_mark: 完整 | :white_check_mark: 完整 |
| 2. 品类分布 | AI 推断 | AI 推断 | AI 推断 | :white_check_mark: 精确 |
| 3. 品味画像 | 基础版 | 基础版 | :white_check_mark: 完整 | :white_check_mark: 完整 |
| 4. 高分书目 | :x: | :x: | :white_check_mark: | :white_check_mark: |
| 5. 演化脉络 | :x: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| 6. 知识网络 | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| 7. 书单推荐 | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| 8. 有趣的洞察 | :x: | 部分 | :white_check_mark: | :white_check_mark: |
| 9. 开创价值 | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| 10. 附录 | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |

## 快速开始

### 方式一：Claude Code（推荐）

**第 1 步**：创建 skill 目录
```bash
mkdir -p ~/.claude/skills/reading-analyst
```

**第 2 步**：下载 skill 文件
```bash
# 中文版
curl -o ~/.claude/skills/reading-analyst/skill.md \
  https://raw.githubusercontent.com/renee-z/reading-analyst-skill/main/skill_cn.md
```

或英文版：
```bash
curl -o ~/.claude/skills/reading-analyst/skill.md \
  https://raw.githubusercontent.com/renee-z/reading-analyst-skill/main/skill.md
```

**第 3 步**：使用！
```
# 在 Claude Code 中，直接提供你的阅读记录：
"这是我的阅读书单，请帮我生成阅读分析报告"
```

当你提供阅读记录并要求分析时，skill 会自动触发。

### 方式二：任何 AI 工具

这个 skill 适用于**任何 AI 助手** —— Claude.ai、ChatGPT、Gemini 或其他 LLM：

1. 打开 [`skill_cn.md`](skill_cn.md)（或英文版 [`skill.md`](skill.md)）
2. 复制全部内容
3. 粘贴到你的 AI 对话中
4. 然后提供你的阅读记录，要求生成分析报告

> **提示**：为获得最佳效果，先粘贴 skill 内容，然后在下一条消息中提供阅读数据。

## 示例输出

查看 [examples/sample-report.md](examples/sample-report.md)，其中展示了真实报告的 4 个核心章节片段：
- 第三章：品味画像（含人物关键词）
- 第六章：知识网络 30 维度雷达图
- 第七章：双书单推荐
- 第九章：阅读的开创价值

## 语言版本

- **中文版 Skill**：[`skill_cn.md`](skill_cn.md)
- **英文版 Skill**：[`skill.md`](skill.md)
- **英文 README**：[`README.md`](README.md)

## 许可证

[MIT](LICENSE) —— 自由使用、修改、分享。
