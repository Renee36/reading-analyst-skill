# Reading Analyst Skill

[![Works with Claude Code](https://img.shields.io/badge/Works%20with-Claude%20Code-blueviolet?logo=anthropic)](https://claude.ai/claude-code)
[![Works with Any LLM](https://img.shields.io/badge/Also%20works%20with-Any%20LLM-green)](#method-2-any-ai-tool)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**Turn years of reading records into a 10-chapter personal reading intelligence report.**

[中文版 README](README_CN.md)

---

## What Makes It Different

| Feature | Reading Analyst Skill | Smart Reading Tracker | CastReader | Generic Book Report |
|---------|----------------------|----------------------|------------|-------------------|
| 10-chapter structured analysis | :white_check_mark: | :x: | :x: | :x: |
| 30-dimension knowledge radar | :white_check_mark: | :x: | :x: | :x: |
| Dual book recommendations (fill gaps + deepen passions) | :white_check_mark: | :x: | :x: | :x: |
| Taste profile with character keywords | :white_check_mark: | :x: | :x: | :x: |
| Creative value analysis | :white_check_mark: | :x: | :x: | :x: |
| Works offline / local | :white_check_mark: | Depends | :x: | Depends |
| Multi-year evolution timeline | :white_check_mark: | :x: | :x: | :x: |
| Input: just book titles | :white_check_mark: | Needs ISBN | Needs ISBN | Varies |

## Features

- **Taste Profiling** — Distills your reading persona with character keywords (e.g., `methodology enthusiast` `scientific aesthetics` `long-term thinker`)
- **30-Dimension Knowledge Radar** — Maps your reading against the full human knowledge landscape using UNESCO + Library of Congress Classification
- **Dual Book Recommendations** — Book List A fills your knowledge gaps; Book List B deepens your passions
- **Evolution Timeline** — Traces how your reading interests migrated over the years
- **Fascinating Insights** — Surfaces hidden patterns: white whale books, cultural undercurrents, volume leaps
- **Creative Value Analysis** — Reveals what unique value your reading accumulation can create

## What You Get: The 10-Chapter Report

| Chapter | Title | What It Covers |
|---------|-------|---------------|
| 1 | Overview & Statistics | Time span, totals, annual trend bar chart |
| 2 | Category Distribution | Sorted breakdown with percentages |
| 3 | Taste Profile | One-liner persona + character keywords + taste traits with evidence |
| 4 | Top-Rated Books | 15-25 highest-rated books with pattern analysis |
| 5 | Evolution Timeline | 3-6 reading phases, turning points, predictions |
| 6 | Knowledge Network | 8 domains × 30 dimensions, radar chart, gap analysis |
| 7 | Book Recommendations | 10 gap-filling + 10 passion-deepening books |
| 8 | Fascinating Insights | 5-7 hidden data discoveries |
| 9 | Creative Value | Unique knowledge combos + output directions |
| 10 | Appendix | Complete book list by year (optional) |

## Input Requirements

You can start with **just book titles** — the more data you provide, the richer the report.

### Input Tiers

| Input Level | What You Provide | Chapters Available | Coverage |
|-------------|-----------------|-------------------|----------|
| **Minimum** | Book titles only | Ch1 (partial), Ch2, Ch3 (basic), Ch6, Ch7, Ch9 | ~6/10 |
| **Recommended** | Titles + year read | + Ch1 (full), Ch5 (evolution), Ch8 (insights) | ~8/10 |
| **Complete** | Titles + year + rating + category | All 10 chapters at full depth | 10/10 |

### Chapter Availability by Input

| Chapter | Titles Only | + Year | + Rating | + Category |
|---------|:-----------:|:------:|:--------:|:----------:|
| 1. Overview & Statistics | Partial | :white_check_mark: Full | :white_check_mark: Full | :white_check_mark: Full |
| 2. Category Distribution | AI-inferred | AI-inferred | AI-inferred | :white_check_mark: Precise |
| 3. Taste Profile | Basic | Basic | :white_check_mark: Full | :white_check_mark: Full |
| 4. Top-Rated Books | :x: | :x: | :white_check_mark: | :white_check_mark: |
| 5. Evolution Timeline | :x: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| 6. Knowledge Network | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| 7. Book Recommendations | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| 8. Fascinating Insights | :x: | Partial | :white_check_mark: | :white_check_mark: |
| 9. Creative Value | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |
| 10. Appendix | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: |

## Quick Start

### Method 1: Claude Code (Recommended)

**Step 1**: Create the skill directory
```bash
mkdir -p ~/.claude/skills/reading-analyst
```

**Step 2**: Copy the skill file
```bash
# Download directly
curl -o ~/.claude/skills/reading-analyst/skill.md \
  https://raw.githubusercontent.com/renee-z/reading-analyst-skill/main/skill.md
```

Or for Chinese version:
```bash
curl -o ~/.claude/skills/reading-analyst/skill.md \
  https://raw.githubusercontent.com/renee-z/reading-analyst-skill/main/skill_cn.md
```

**Step 3**: Use it!
```
# In Claude Code, simply provide your reading records:
"Here's my reading list, please generate a reading analysis report"
```

The skill triggers automatically when you provide reading records and request analysis.

### Method 2: Any AI Tool

This skill works with **any AI assistant** — Claude.ai, ChatGPT, Gemini, or other LLMs:

1. Open [`skill.md`](skill.md) (or [`skill_cn.md`](skill_cn.md) for Chinese)
2. Copy the entire content
3. Paste it into your AI conversation
4. Then provide your reading records and ask for analysis

> **Tip**: For best results, paste the skill content first, then your reading data in a follow-up message.

## Sample Output

See [examples/sample-report.md](examples/sample-report.md) for excerpts from a real report, showcasing:
- Chapter 3: Taste Profile with character keywords
- Chapter 6: Knowledge Network 30-dimension radar chart
- Chapter 7: Dual book recommendations
- Chapter 9: Creative Value analysis

## Language

- **English skill**: [`skill.md`](skill.md)
- **Chinese skill (中文版)**: [`skill_cn.md`](skill_cn.md)
- **Chinese README**: [`README_CN.md`](README_CN.md)

## License

[MIT](LICENSE) — use it, modify it, share it.
