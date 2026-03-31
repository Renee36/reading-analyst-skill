# Reading Analyst Report Skill

## Description
From the user's reading records (Excel / CSV / text list), automatically extract book data and generate a structured personal reading analysis report (Markdown format). The report covers data statistics, taste profiling, knowledge network assessment, book recommendations, personalized insights, and creative value analysis.

## Trigger Conditions
Triggered when the user provides a reading list/book records and requests reading analysis, reading reports, taste profiling, or knowledge assessment.

## Input Requirements
The user should provide reading records in any of the following formats:
- **Excel file**: containing fields such as title, category, completion status, rating (field names are flexibly recognized)
- **CSV / text list**: at minimum containing book titles, ideally with categories and ratings
- **Manual list**: directly listing book titles

Key fields (collect as many as possible, not all required):
| Field | Description | Necessity |
|-------|-------------|-----------|
| Title | Book name | **Required** |
| Year | Year read/planned | Strongly recommended |
| Category | Book genre (e.g., self-help, fiction, professional) | Strongly recommended |
| Status | Completed / Reading / Unread | Recommended |
| Rating | User score | Recommended |
| Notes | One-line review or key takeaway | Optional (enables deeper insights) |

## Data Processing Pipeline

### Step 1: Data Extraction & Cleaning
1. Read all sheets/data sources, identify header rows (field names may be in different rows)
2. Note that column structures may differ across year sheets; adapt per sheet
3. Only extract rows where the title begins with a book marker (e.g., 「《」for Chinese, or standard title formats)
4. **Deduplication**: the same book may appear in multiple years (carried over if unfinished); use the earliest year marked "completed" as the definitive year to avoid double-counting
5. Distinguish completed vs. unfinished books, tallying each separately

### Step 2: Statistical Analysis
Calculate the following metrics:
- Total books read (after deduplication)
- Annual reading volume distribution
- Category distribution (count + percentage)
- Rating statistics (number of rated books, average, highest, lowest)
- Average rating per category

### Step 3: Internal Consistency Pre-Check
Before generating the report, build the following data indices to ensure all chapters reference the same data source:
- **Top-rated books index**: list all perfect-score and high-score (e.g., ≥4.8) books with title, rating, category, year. This index must be referenced consistently in Chapter 3 (Taste Profile) and Chapter 4 (Top-Rated Books table).
- **Annual statistics index**: books read per year; Chapter 1 trend chart and Chapter 5 evolution timeline must match.
- **Category-dimension mapping table**: each book mapped to the 30 knowledge network dimensions, used for Chapter 6 ratings.

### Step 4: Generate Report
Output the complete Markdown report following the ten-chapter structure below.

---

## Report Structure Template (Ten Chapters)

### Chapter 1: Overview & Statistics
- Time span, total books read, number of rated books, average score, number of categories covered
- **Annual reading volume trend** (visualized with `█░` bar chart), example format:

```
2022 ███████████████████████████ 27 ← strong comeback
2023 ███████████████████████████ 27
2024 ██████████████████████████████████░ 34
2025 ██████████████████████████████████████████████████░ 50 ← peak
```

- One-sentence summary of the trend (e.g., "U-shaped curve — decline then rise, with 2022 as the turning point")

### Chapter 2: Reading Category Distribution
- Table: Category | Count | Percentage | Notes
- **Sorted by count in descending order**
- Percentages should sum to approximately 100% (rounding tolerance ±2%)
- Long-tail categories may be merged into an "Other" row with details noted

### Chapter 3: Taste Profile

Based on data, distill the reader's reading persona, including:

#### Core Profile
- **One-line summary** (e.g., "A rationally-driven self-improvement reader with humanistic warmth")
- **Character keywords** (6-10 words), displayed in inline code format, e.g.:
  `methodology enthusiast` `scientific aesthetics` `classicist` `action-oriented` `long-term thinker` `cross-cultural curiosity`

#### Taste Traits (3-5)
Each trait must include:
- **Trait name** (e.g., "Methodology Devotee", "Scientific Worldview")
- **Specific evidence**: cite specific book titles and data (e.g., "the 'self-management' thread alone spans 15+ books")
- **Rating evidence**: cite specific ratings (e.g., "Atomic Habits ★5, Peak Mind ★5"), **must match the Chapter 4 top-rated table exactly**
- **Taste judgment**: summarize what this trait reveals about the reader's preferences

**⚠ Data Consistency Requirement**: Any rating-related statement in the taste profile (e.g., "there are X books rated 5 stars, namely...") must first cross-reference the top-rated books index built in Step 3, ensuring the book list and count are perfectly consistent. This is the most common source of data errors.

### Chapter 4: Top-Rated Books
- Table listing the 15-25 highest-rated books (covering down to ≥4.8)
- Table columns: Rating | Title | Category | Year
- **Sorted by rating descending**, then by year descending for ties
- **Summary narrative** (2-3 paragraphs) answering:
  - Which years do perfect-score books cluster in? What does this indicate?
  - What types of books most often receive high ratings?
  - Common qualities of top-rated books (e.g., evidence-based, strong narrative, paradigm-shifting)
  - What do the top-rated books reveal about what the reader values most?

### Chapter 5: Reading Evolution Timeline
- Divide reading history into phases (typically 3-6 phases)
- Table: Phase Name | Years | Keywords | Description
- Identify turning points and growth spurts
- **Summary narrative** (2-3 paragraphs) answering:
  - What is the migration path of reading interests? (e.g., professional skills → literary aesthetics → self-management → scientific cognition → classical humanities)
  - What events or life stages triggered qualitative shifts?
  - Looking at the entire evolution, where is the reader's reading headed?
  - Predict the next likely reading phase

### Chapter 6: Knowledge Network Panoramic Assessment

**This is the core chapter of the report. It must comprehensively cover the entire human knowledge landscape, not limited to categories the user has already read.**

#### Classification Logic

Before the assessment, explain the 8 domains and 30 dimensions classification basis:

> **Classification Framework**
>
> This assessment uses a cross-reference framework of **UNESCO International Standard Classification of Education (ISCED)** and the **Library of Congress Classification (LCC)**, adapted for personal reading contexts:
>
> | Domain | Classification Basis | Coverage |
> |--------|---------------------|----------|
> | I. Self-Growth & Life Skills | LCC BF (Applied Psychology) + L (Education) + practical living | Knowledge for personal effectiveness and daily life |
> | II. Humanities & Literature | LCC P (Language & Literature) + UNESCO "Humanities" | Literary works by genre and region |
> | III. Social Sciences | UNESCO "Social Sciences" + LCC H/J/K | Disciplines studying how human society operates |
> | IV. Natural Sciences & Technology | UNESCO "Natural Sciences" + LCC Q/T | Disciplines studying the natural world and technology |
> | V. History & Geography | LCC C/D/E/F/G | Time dimension (history) + spatial dimension (geography) |
> | VI. Philosophy & Religion | LCC B (Philosophy/Religion) | Knowledge systems addressing ultimate questions |
> | VII. Arts & Aesthetics | LCC N/M (Fine Arts / Music) + UNESCO "Arts" | Various forms of human aesthetic expression |
> | VIII. Business & Career | LCC HB-HJ (Economics/Management) + professional skills | Knowledge for career development and business practice |
>
> Each domain's dimension breakdown follows the **MECE principle** (Mutually Exclusive, Collectively Exhaustive), ensuring:
> - Every book the user has read can be assigned to a dimension
> - No major branch of human knowledge is omitted
> - Blank areas are equally important as covered areas and must be assessed

#### Assessment Dimensions Checklist (Complete)

**I. Self-Growth & Life Skills** (8 dimensions)
Self-Management & Habits / Brain Science & Cognition / Negotiation & Communication / Health & Body Management / Mind-Body-Spirit Practice / Personal Finance & Investing / Cooking & Food Culture / Home & Lifestyle Aesthetics

**II. Humanities & Literature** (6 dimensions)
Domestic Contemporary Literature / Foreign Classic Literature / Regional Specialty Literature (e.g., Japanese Literature, adapted to reader preference) / Science Fiction / Poetry & Essays / Drama & Screenwriting

**III. Social Sciences** (7 dimensions)
Psychology / Economics / Political Science & International Relations / Legal Literacy / Sociology & Anthropology / Gender Studies / Education Studies

**IV. Natural Sciences & Technology** (6 dimensions)
Biology & Evolution / Physics & Astronomy / Mathematics / Chemistry & Materials / Earth & Environmental Science / Computer Science & AI

**V. History & Geography** (3 dimensions)
World History / National History / Geography & Travel

**VI. Philosophy & Religion** (3 dimensions)
Western Philosophy / Eastern Philosophy / Religious Studies

**VII. Arts & Aesthetics** (4 dimensions)
Painting & Visual Arts / Music / Architecture & Design / Film & Media

**VIII. Business & Career** (4 dimensions)
Project Management / Business & Entrepreneurship / Leadership & Management / Writing & Expression

> **Note**: The "Regional Specialty Literature" dimension can be renamed based on the reader's actual preference (e.g., if a reader heavily reads Japanese literature, name it "Japanese Literature").

#### Assessment Format Per Dimension
| Dimension | Rating (★1-5) | Representative Books | Assessment Notes |

#### Rating Criteria
- ★★★★★ (9-10 pts): Exceptional — systematic understanding with cross-validated multi-book coverage
- ★★★★☆ (7-8 pts): Solid — multiple books read with reasonable depth
- ★★★☆☆ (5-6 pts): Basic — several related books read
- ★★☆☆☆ (2-4 pts): Weak — only sporadic exposure
- ★☆☆☆☆ (1 pt): Blank — no relevant reading

#### Sorting Rule
**Within each domain, dimensions must be sorted by rating in descending order.** This lets the reader immediately see their strengths and weaknesses within each domain.

#### Required Sub-Sections

**A. Eight Domains × 30 Dimensions Detailed Assessment**
- 8 domains grouped, one table per group
- Dimensions within each group sorted by rating descending
- Every dimension must have representative books (write "None" if blank) and assessment notes

**B. Knowledge Network Panoramic Radar Chart (Text Version)**
- Use `█░` bar chart to display all 30 dimensions on a 1-10 scale
- Grouped by domain with separator lines between groups
- Annotate extreme values (e.g., `← dominant`, `← blank`, `← growing`)
- Example format:

```
═══════════════════════════════════════════════════════════
  I. Self-Growth & Life Skills                    Score
═══════════════════════════════════════════════════════════
  Self-Management & Habits  ██████████ 10/10  ← dominant
  Brain Science & Cognition ████████░░  8/10
  Personal Finance          █░░░░░░░░░  1/10  ← blank
───────────────────────────────────────────────────────────
```

**C. Gap Overview: Completely Blank Domains (1/10)**
- Table: Blank Domain | Why It Matters | One Starter Book Recommendation
- "Why It Matters" should connect to the reader's life context (e.g., "parent of two children", "working professional")

**D. Summary**
- Characterize the knowledge structure shape (e.g., "inverted-T", "lopsided", "balanced") with a one-sentence explanation
- **30-dimension statistics**: how many dimensions are strengths (≥7), foundational (4-6), weak/blank (1-3), with percentages
- Top 3 priority areas to fill + why

### Chapter 7: Reading Recommendations: Book Lists & Pathways

This chapter contains **two book lists** addressing different needs:

#### Book List A: Filling the Gaps — Essential Knowledge (10 books)

**Selection principle**: Prioritize coverage of domains rated 1 (blank) in Chapter 6; recommend at least 1 starter book per blank domain.

| # | Title | Gap Filled | Recommendation Rationale (connection to reader's taste) |

**Requirements**:
- Design a reading path upfront (e.g., life essentials → social awareness → aesthetic expansion → world understanding)
- Rationale must explain "why this book and not another" — connecting to the reader's existing preferences (e.g., "given your taste for evidence-based + narrative style" → recommend specific book)
- If there are N blank domains, cover at least N (if >10, prioritize the 10 most important)
- **Confirm the reader has not already read any recommended book**

#### Book List B: Deepening Passions — Advanced Reading in Current Interests (10 books)

**Selection principle**: Based on the reader's most active/highest-rated domains, recommend books that take existing knowledge "to the next level."

| # | Title | Domain Deepened | Connection (how it links to books already read) |

**Requirements**:
- Each recommendation must explain which previously-read book it connects to, example format:
  > "After reading Atomic Habits ★5 and Peak Mind ★5, this book offers Nobel Prize-level cognitive science explaining 'why your brain works the way it does'"
- Cover the reader's 3-5 highest-rated domains
- If the reader has a "white whale list" (books planned for years but never finished), include them with a note that "now is the perfect time"
- **Confirm the reader has not already read any recommended book**

### Chapter 8: Fascinating Insights

Uncover 5-7 hidden discoveries in the data, drawing from angles such as:
- **White whale books**: books that appear repeatedly over years but remain unfinished
- **Turning points**: sudden shifts in reading volume/category/quality and their likely triggers
- **Plan vs. reality**: patterns in the gap between annual reading goals and actual completions
- **Review style**: what the reader's book reviews/notes reveal about their reading approach (do they "read" books or "use" books?)
- **Cultural undercurrents**: hidden cultural preferences (e.g., a Japanese culture affinity, a national literature bias)
- **Management style**: unique reading management methods (e.g., Gantt charts, person-day calculations)
- **Volume leaps**: exponential reading growth from a specific year onward

**Writing requirements**:
- Every insight must be supported by **specific data and book titles** — no empty statements
- Highlight key findings in **bold**
- Number each insight with a subheading

### Chapter 9: Creative Value of Your Reading

This chapter answers a higher-order question: **What unique value can this reading accumulation create for the reader? How can it help others?**

#### 9.1 Your Unique Knowledge Combination
- List the reader's cross-domain knowledge intersections (using `A × B × C × D` format)
- Analyze the rarity of this combination in the general population
- Explain why the intersection of these domains produces unique perspectives (not just "you know a lot," but explaining the chemical reaction of knowledge stacking)

#### 9.2 Potential Output Directions
Based on reading accumulation, propose 3-5 specific knowledge output directions, each including:
- **Direction name** (e.g., "Reading Management Through Project Management Methods")
- **Why you can do it**: connection to existing knowledge
- **Target audience**: specifically describe who would benefit
- **Format**: book / course / column / community, etc.

#### 9.3 How to Help More People
- Which of the reader's experiences/methods/paths are replicable
- What is the most impactful entry point for sharing (usually a transformation story, not a book list)
- Who is the reader best positioned to help (combining their career, life roles)

**Writing requirements**:
- Must be based on data analysis from previous chapters — no speculation
- Output direction suggestions must be specific and actionable — avoid vague statements like "you could do many things"
- Connect to the reader's professional background and life roles (e.g., parent, professional)

### Chapter 10: Appendix — Complete Book List (Optional)
- List all completed books by year
- Include: Year, Title, Category, Rating (if available)
- This chapter can be lengthy; include based on user preference
- If the book count is very large (>200), suggest the user export it separately as Excel/CSV

---

## Output Requirements

1. **Format**: Markdown file (`.md`)
2. **Language**: Match the language of the user's reading records (default to the language of the input data)
3. **Save location**: Ask the user for their preferred save path; default to Desktop
4. **File name format**: `{username}_Reading_Analysis_Report_{start_year}-{end_year}.md`

## Quality Checklist

Before generating the report, verify the following:

### Data Accuracy
- [ ] Books are deduplicated — no book counted more than once
- [ ] Annual statistics only include completed books
- [ ] Category distribution percentages sum to approximately 100%

### Cross-Chapter Consistency (⚠ Most Common Error Source)
- [ ] **Taste Profile (Ch3) rating references match the Top-Rated Books table (Ch4) exactly**
  - Example: If Ch3 says "8 books rated 5 stars," then Ch4 must show exactly 8 five-star books
  - Example: If Ch3 says "Book X ★5," then Ch4 must show that book with a 5-star rating
- [ ] Annual reading trend (Ch1) matches evolution timeline (Ch5) year data
- [ ] Knowledge network radar chart scores (Ch6-B) match detailed assessment tables (Ch6-A)

### Structural Completeness
- [ ] Ch4 top-rated books table is followed by summary narrative paragraphs
- [ ] Ch5 evolution timeline table is followed by summary narrative paragraphs
- [ ] Ch6 includes classification logic explanation (UNESCO + LCC framework)
- [ ] Ch6 covers all 30 dimensions, not just categories the user has read
- [ ] **Ch6 dimensions within each domain are sorted by rating descending**
- [ ] Ch6 blank domains (1 pt) are all identified with starter book recommendations
- [ ] Ch6 summary includes 30-dimension statistics and priority fill directions

### Recommendation Quality
- [ ] **Book List A (filling gaps) covers all 1-point blank domains**
- [ ] Book List A includes a reading path design
- [ ] **Book List B (deepening passions) explicitly connects each book to the reader's top-rated books**
- [ ] All 20 recommended books are confirmed unread by the user

### Content Depth
- [ ] Every insight (Ch8) is supported by specific book titles and data
- [ ] Creative value (Ch9) output directions are specific and actionable with target audiences
- [ ] Taste Profile (Ch3) includes 6-10 character keywords

## Core Principles

1. **Comprehensiveness**: Knowledge assessment must cover the full human knowledge landscape; blank areas are as important as covered ones
2. **Data-driven**: All conclusions must be backed by book data — no unfounded speculation
3. **Internal consistency**: Data references across chapters must be consistent with no contradictions. Build unified data indices before generating the report
4. **Personalization**: Taste profiles and insights must be specific to this individual reader — no template language
5. **Actionable**: Book recommendations split into "fill the gaps" and "deepen your passions" tracks, each with clear recommendation logic
6. **Honest assessment**: Do not shy away from blank areas — honestly mark 1-point dimensions
7. **Future-oriented**: Don't just analyze the past — answer "what value can this reading create"
