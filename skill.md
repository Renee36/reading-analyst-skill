---
name: analyzing-reading
description: "Generates a structured 10-chapter reading intelligence report from personal reading records (Excel/CSV/text). Covers taste profiling with character keywords, 30-dimension knowledge radar (UNESCO + LCC framework), dual book recommendations (gap-filling + passion-deepening), evolution timeline, and creative value analysis. Use when the user provides a book list, reading log, or reading records and requests reading analysis, taste profiling, knowledge assessment, or book recommendations."
---

# Reading Analyst Skill

## Input requirements

Accepts reading records in Excel, CSV, text list, or manually listed book titles.

Key fields (collect as many as possible):

| Field | Necessity |
|-------|-----------|
| Title | **Required** |
| Year read | Strongly recommended |
| Category | Strongly recommended |
| Completion status | Recommended |
| Rating | Recommended |
| Notes / one-line review | Optional (enables deeper insights) |

## Data processing workflow

Copy this checklist and track progress:

```
Data Processing:
- [ ] Step 1: Extract & clean data
- [ ] Step 2: Statistical analysis
- [ ] Step 3: Internal consistency pre-check
- [ ] Step 4: Generate 10-chapter report
- [ ] Step 5: Quality verification
```

### Step 1: Extract & clean data
1. Read all sheets/data sources, adapt per-sheet column structures
2. Extract valid book entries (title field must be present)
3. **Deduplicate**: same book across multiple years → use earliest "completed" year
4. Separate completed vs. unfinished books

### Step 2: Statistical analysis
Calculate: total books read (deduplicated), annual volume distribution, category distribution (count + %), rating statistics (count, average, highest, lowest), average rating per category.

### Step 3: Internal consistency pre-check

**Build these indices BEFORE generating any chapter** — this prevents the most common error (cross-chapter data contradictions):

- **Top-rated books index**: all books rated ≥4.8 with title, rating, category, year → used in Ch3 and Ch4
- **Annual statistics index**: books per year → used in Ch1 and Ch5
- **Category-dimension mapping**: each book → one of 30 knowledge dimensions → used in Ch6

### Step 4: Generate 10-chapter report

Follow the structure below. For Ch6 knowledge dimensions reference, see [DIMENSIONS.md](DIMENSIONS.md).

### Step 5: Quality verification

Run the quality checklist at the end of this file before delivering.

---

## Report structure (10 chapters)

### Ch1: Overview & Statistics
- Time span, totals, rated book count, average score, category count
- **Annual trend bar chart** using `█░` blocks, with one-sentence trend summary
- Example: `2024 ██████████████████████████████████░ 34`

### Ch2: Category Distribution
- Table: Category | Count | % | Notes — sorted by count descending, sum ≈100%

### Ch3: Taste Profile
- **One-line persona** + **6-10 character keywords** in inline code (e.g., `methodology enthusiast` `long-term thinker`)
- 3-5 taste traits, each with: trait name, specific book evidence, rating evidence (**must match Ch4 exactly**), taste judgment
- ⚠ Cross-reference the top-rated books index before citing any rating data

### Ch4: Top-Rated Books
- Table of 15-25 highest-rated books (≥4.8): Rating | Title | Category | Year — sorted by rating desc
- 2-3 paragraph summary: year clustering patterns, high-score book qualities, what reader values most

### Ch5: Evolution Timeline
- 3-6 reading phases table: Phase | Years | Keywords | Description
- 2-3 paragraph summary: interest migration path, turning points, predicted next phase

### Ch6: Knowledge Network Assessment

**Core chapter — must cover the full human knowledge landscape, not just what the reader has read.**

Uses 8 domains × 30 dimensions framework. For the complete dimension list, classification logic, and rating criteria, see [DIMENSIONS.md](DIMENSIONS.md).

Required sub-sections:
- **A. Detailed assessment**: 8 domain tables, dimensions sorted by rating desc, every dimension has representative books or "None"
- **B. Radar chart**: `█░` bar chart for all 30 dimensions (1-10 scale), grouped by domain, annotate extremes (`← dominant`, `← blank`)
- **C. Gap overview**: table of all blank domains (1/10) with "Why it matters" (connect to reader's life context) + starter book
- **D. Summary**: knowledge structure shape label (e.g., "inverted-T"), 30-dimension stats (strengths/foundational/weak counts), top 3 priority fill directions

### Ch7: Book Recommendations

**Book List A — Filling Gaps (10 books)**:
- Cover all Ch6 blank domains (1-point), design a reading path
- Each book: why this one specifically, connected to reader's taste
- **Confirm reader hasn't read it**

**Book List B — Deepening Passions (10 books)**:
- Based on reader's 3-5 highest-rated domains
- Each book must explain connection to a specific high-rated book already read (e.g., "After reading X ★5, this book takes it further by...")
- **Confirm reader hasn't read it**

### Ch8: Fascinating Insights
- 5-7 data-driven discoveries (white whale books, turning points, plan vs. reality, cultural undercurrents, volume leaps)
- Every insight backed by **specific book titles and data**

### Ch9: Creative Value
- **9.1 Unique knowledge combination**: cross-domain intersections in `A × B × C` format, rarity analysis
- **9.2 Output directions**: 3-5 specific proposals (name, why you can do it, target audience, format)
- **9.3 How to help others**: replicable methods, best entry point, target audience — connect to reader's career and life roles

### Ch10: Appendix (Optional)
- Complete book list by year. If >200 books, suggest separate export.

---

## Output requirements

- **Format**: Markdown file (`.md`)
- **Language**: match input data language
- **Save path**: ask user, default to Desktop
- **File name**: `{username}_Reading_Analysis_{start_year}-{end_year}.md`

## Quality checklist

```
Quality Verification:
- [ ] Books deduplicated, no double-counting
- [ ] Category percentages sum ≈100%
- [ ] Ch3 rating claims match Ch4 table exactly (most common error!)
- [ ] Ch1 annual data matches Ch5 timeline
- [ ] Ch6 radar scores match Ch6 detail tables
- [ ] Ch6 covers all 30 dimensions, sorted by rating desc within each domain
- [ ] Ch6 all blank domains identified with starter recommendations
- [ ] Book List A covers all 1-point blank domains
- [ ] Book List B connects each book to a specific high-rated book already read
- [ ] All 20 recommended books confirmed unread
- [ ] Ch3 has 6-10 character keywords
- [ ] Ch8 every insight has specific book titles and data
- [ ] Ch9 output directions are specific and actionable
```

## Core principles

1. **Comprehensiveness**: knowledge assessment covers the full human knowledge landscape — blanks are as important as strengths
2. **Data-driven**: all conclusions backed by book data, no speculation
3. **Internal consistency**: build unified data indices before generating — no cross-chapter contradictions
4. **Personalization**: taste profiles and insights must be specific to this reader, no template language
5. **Actionable**: dual-track recommendations with clear logic per book
6. **Honest**: do not shy away from blank areas
7. **Future-oriented**: answer "what value can this reading create"

## Error handling

- **<10 books**: warn user, skip Ch5 and Ch8 if data insufficient
- **No ratings**: skip Ch4, generate Ch3 from category patterns only, note limitation
- **No years**: skip Ch5, Ch1 shows totals only without trend chart, note limitation
- **Unrecognizable format**: ask user to clarify, provide example format
- **Ambiguous duplicates** (different editions/translations): list ambiguous entries, ask user to confirm
- **>500 books**: generate Ch1-Ch9 first, Ch10 on request
