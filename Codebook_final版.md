# Track 3 — Codebook v1.0

**Project:** *Shared Core, Different Emphases? A Comparative Analysis of BA/DA Interview Experiences on Nowcoder and Reddit (2023–2026)*  
**Updated:** 2026-11-03  
**Status:** Operational coding guide revised using the 40-item joint Pilot Coding sheet; **not yet independently validated**.  
**Intended use:** Freeze these definitions for the new 150-item independently hand-coded Gold Set. This file is a coding protocol, not a findings report.

## 0. Quick start / 快速填写

1. Read **title + text**. Do **not** derive interview skills from `keyword` (a search term).
2. Code `role_match`, `actual_interview`, `usable_detail` using `1 / 0 / U`.
3. Compute `relevance_status`: all three `1` → `include`; **any `0`** → `exclude`; otherwise → `uncertain`.
4. Only for `include`, code the ten skills; multiple `1`s are allowed. For `exclude` and `uncertain`, enter `NA`/blank for skills.
5. Complete process fields only when supported by text. Record a short verbatim `evidence_text`, a reason in `decision_note`, and `text_completeness`.
6. Two coders must label **the same** formal 150 records independently; preserve separate versions before resolving disagreements.

> **IMPORTANT — pilot `U` versus formal labels:** In the previously revised 40-item pilot, skill `0` values were changed to `U` at the team's request. Those `U` entries consequently combine *not reported* with *genuinely unclear*. **Do not use them unchanged as formal validation labels.** For Gold Set v1.0, recover the distinction: `1` = explicitly reported; `0` = not reported **in the available text**; `U` = text is genuinely too ambiguous/incomplete to decide. A `0` does **not** claim the real interview did not test that skill. No additional variables are required.

## 1. Research scope and units

- **Primary research question:** How do skills and competencies **reported in BA/DA interviews** differ between public posts on Nowcoder and Reddit?
- **Unit:** one unique platform **post**, not one question or interview. One post may contain multiple questions, rounds, or interviews; flag mixed interviews in `decision_note` and avoid treating them as multiple independent observations.
- **Platform:** `Reddit` or `Nowcoder`. This records the **source of the post**, **not** the interview country or employer nationality.
- **Study window:** posts published 2023-01-01 through 2026-09-22, as established for the current corpus. `date` is the **post date**, not necessarily the actual interview date.
- **Available source fields:** `keyword`, `title`, `text`, `date`, `url`; keep `record_id`, `platform`, `source_row` for traceability. Preserve platform-specific originals in raw datasets.
- **Main outcomes:** `sql`, `programming`, `statistics`, `machine_learning`, `business_case`, `product_metrics`, `bi_visualization`, `behavioral`, `project_experience`, `ai_tool_assessment`.
- **Supplementary:** `rounds_reported`, `round_count`, `assessment_format`, `role_level`, `company_type`, `text_completeness`. **No new column is required.**

## 2. Stage A — Eligibility / 是否纳入分析

| Field | `1` — yes | `0` — no | `U` — uncertain |
|---|---|---|---|
| `role_match` | Clearly an interview for **Business Analyst, Data Analyst, BI Analyst, analytics-focused Product Analyst, or an explicit analytics analyst role** (商业分析/数据分析/风控数据分析等). | Clearly **back-end/software engineer, Data Engineer, ML/LLM algorithm engineer, general Product Manager, game/product operations, general sales strategy, generic management trainee, investment analyst, materials/failure-analysis engineer**, etc., with no distinct target analytics analyst role. | Role not identified, or mixed/blended description cannot separate analyst work from engineering/product/other roles. |
| `actual_interview` | Actual interview/test occurred, described via asked questions, tests, or interview process. Explicit concrete second-hand reports can count; mention source in notes. | Only preparation questions, prospective interviews, job seeking, advice, advertising, hypothetical practice questions, or unrelated industry discussion. | Wording or truncated snippet cannot show whether the assessment actually happened. |
| `usable_detail` | At least **one** concrete question, evaluated skill, assessment format, or round/sequence is stated. | Only “I interviewed” / “interview went well” without usable details, or no actual interview information. | Fragment does not let the coder decide. |

**Derived field:** `relevance_status = include` only if all three equal `1`; `exclude` if any equals `0`; `uncertain` otherwise. Keep `uncertain` out of the main descriptive denominator until resolved.

### Pilot-grounded boundary rules

- **N0082** (美团后端开发岗), **N0195** (百度大模型算法), **N0189** (游戏产品运营), **N0326** (产品经理), **N0294** (商业仕官生) → exclude from the primary BA/DA comparison even though they contain real interviews or business/technical questions.
- **N0116** (数据开发与数据分析混合面经), **N0280** (数据产品实习), **R0135** (multi-role Data Science / Engineering / Analytics discussion) → `role_match = U` unless the analyst interview can be distinctly identified. Do not automatically force inclusion.
- **N0171** (数据分析), **N0322** (风控数据分析), **N0137** (数据分析实习) → analyst roles, eligible **when** the other two Stage A fields also equal `1`.
- **R0205** (preparing for an upcoming DA interview) → `role_match = 1`, but `actual_interview = 0`, so exclude. Do not automatically set all three Stage A flags to `0` just because the final status is exclude.
- **R0365** (SEC/EDGAR data-quality post) and **R0348** (work-related SaaS analytics case) → actual interview = `0`; a *real-world business case* is not necessarily an *interview case*.
- **N0386** (data-analyst written test on data structures) can be `include` even if none of the ten tracked skill groups is explicitly supported; do not invent `sql=1` or `programming=1` to force it into a category. Preserve the test description in `evidence_text` and `decision_note`.

## 3. Stage B — Assessment codes / 面试考察内容

**Only for `include` posts:** `1` = concrete evidence the interviewer assessed the category; `0` = **not reported in readable available text**, not evidence of absence in the whole interview; `U` = evidence is too truncated, ambiguous, or uninterpretable to determine the category. For `exclude` or `uncertain`, skills = `NA`/blank, not zero. More than one skill can be `1` in a single post.

| Skill field | Code `1` when the actual interview explicitly… | Do **not** code `1` merely because… |
|---|---|---|
| `sql` | asked SQL queries, JOIN/window functions or SQL written/live tests | SQL appears in search keyword, resume, or preparation advice |
| `programming` | asked Python/R code, live coding, algorithm implementation, or programming knowledge | candidate uses Python at work, lists it on CV, or studied it; a vague “technical test” alone is insufficient |
| `statistics` | asked probability, inference, hypothesis tests, experimental design, A/B testing, regression | data analysis generally involves numbers; A/B experimentation appears only as everyday work |
| `machine_learning` | asked ML concepts, model choice, training, feature engineering, evaluation, or deep-dived into ML project methodology | author studied ML; ML appears only as job history or project list |
| `business_case` | gave an **interview** business problem to diagnose, prioritize or recommend action: GMV/revenue drop, investment/market choices, business performance | text presents a non-interview industry case or speculative practice exercise |
| `product_metrics` | explicitly assessed retention, conversion, funnels, user growth, product KPIs or metric construction | a vague “build a metric” has no evidence of product/user metrics; GMV alone does not automatically qualify |
| `bi_visualization` | tested Excel, Power BI, Tableau, dashboarding or visualization/data presentation | tools are only on the candidate’s resume or used at work |
| `behavioral` | asked motivation, teamwork, conflict, communication, leadership, behavioral scenarios or relevant situational answers | only “tell me about yourself” with no other behavioral assessment |
| `project_experience` | asked to explain/defend/deep-dive internships, past projects, CV or previously delivered analyses | candidate only describes past work without being questioned |
| `ai_tool_assessment` | asked to use or evaluate ChatGPT/Copilot/LLM/prompting/AI-assisted analytical tools **as an interview assessment** | AI tools are used for interview preparation, general job tasks, industry trends, or ML/LLM training theory (e.g., DPO) without AI-tool-fluency assessment |

### Multiple applicable labels / 易混淆情况

- **SQL + business scenario** → `sql=1` and `business_case=1` when **both** were actually tested.
- **A/B experiment-design question** → `statistics=1`. Add `business_case=1` only if a substantive business decision case is also posed.
- **ML project deep-dive** (e.g., N0171’s “项目机器学习拷打”) → `machine_learning=1` and `project_experience=1` when both are explicitly supported.
- **GMV/revenue drop** → generally `business_case=1`; `product_metrics=1` only when product/user metrics are explicitly assessed.
- **DPO/multimodal model-training principles** → `machine_learning=1` only for an **eligible analyst-role** actual interview; do not confuse with `ai_tool_assessment`. An LLM-engineer role is excluded at Stage A.
- **R0344**: coding questions the applicant **practiced** but the interview did **not** ask do not count as `programming=1`; explicitly reported assessed SQL/case/behavioral items may count.
- **N0386**: a test may be eligible but not map clearly to the ten existing skill fields. Retain evidence; do not create a new variable merely to assign a `1`.

### Handling the previous pilot's all-`U` nonpositives

The 40-item AI-assisted revised workbook deliberately overwrote earlier skill zeros with `U`. **Do not interpret its `U` values as proof that every skill is genuinely uncertain.** That coding convention is a documented pilot limitation. For formal Gold Set labels, use the three meanings above, and if reusing any pilot row, independently reread and recode it rather than mechanically replacing `U` with `0`. In comparative analysis, the statistic is **share of included posts explicitly reporting the skill**, with `U` and snippets disclosed; it is *not* a measure of the true probability an employer tests it.

## 4. Stage C — Interview process and documentation

| Field | Values and decision rule |
|---|---|
| `rounds_reported` | `1` if a particular interview process explicitly states rounds/sequence (一面/二面, screening → technical, etc.); `0` if the available post gives no such round information; `U` if wording is ambiguous. Multiple unrelated interviews are **not** automatically rounds of one company. |
| `round_count` | Positive integer **only if the total rounds for an identifiable process are explicitly supported**; else **blank**. “二面” alone does not prove there were only two total rounds; question numbers do not count as rounds. “7–8 interviews at several companies” is not a single firm’s round_count. |
| `assessment_format` | Use exactly one: `live coding`, `take-home`, `written test`, `case`, `technical Q&A`, `behavioral`, `multiple`, `not reported`, `unknown`. Use `multiple` only when multiple formats explicitly occur. A data-analyst笔试 can be `written test`; do not call it live coding unless actually live. |
| `role_level` | `internship`, `entry`, `experienced`, `unknown`; only when stated or unmistakably described. |
| `company_type` | State a firm **type** in plain words only if reliably evident from the post; otherwise `unknown`. Do not use `0`/`1` in this field. |
| `text_completeness` | `full` only when full content is reasonably established; `snippet` for visibly cut-off excerpts/search snippets; otherwise `unknown`. An ellipsis is a **flag** that may indicate truncation, not a reliable measure of missing length. |
| `evidence_text` | Quote short *actual source* phrases supporting relevance and every positive skill, avoiding invented or “repaired” statements. |
| `decision_note` | Brief explanation, especially for exclusion, `U`, mixed roles, snippet limitations, or uncategorized tests. |
| `coder_id` | For the prior 40, mark **joint pilot / AI-assisted**, not two independent coders. For formal 150, each coder has a separate independent sheet/file and ID. |
| `codebook_version`, `coding_date` | Record the actual version and true date. Never invent earlier dates or imply AI-updated entries were independently hand-coded. |

## 5. Sampling, automation, validation and reporting

1. Preserve **raw**, **technically cleaned** and **analysis-ready** datasets separately. Keep track of removed/flagged duplicates and the previously excluded **32 Reddit records**; they were removed without confirming whether they were valid interviews.
2. The joint 40-item pilot is a **method-development exercise**: **10 include / 27 exclude / 3 uncertain** in its AI-assisted revised file, **not independently validated numbers** and **not** the primary empirical comparison.
3. Sample **at least 150** items from both platforms (e.g., 75 each), ideally avoiding the 40 pilot items used to revise the rules. Include relevant and irrelevant candidates so relevance screening can be validated. Keep fixed seed, `record_id`, `platform`, `url`, and sampling frame.
4. Two human coders must **independently code the same 150 items** with these frozen rules; only afterward compare, compute **percent agreement and Cohen's kappa** (where appropriate), document disagreements, and adjudicate final Gold Set labels. **Joint consensus alone cannot produce inter-coder agreement.**
5. Separately run transparent, reproducible automatic screening/skill extraction on the candidate corpus. Compare automated outputs against the **final human Gold Set** using precision, recall and F1 per relevant category (describe how `U` and `NA` were handled). Do not inspect/fit rules against the held-out validation examples and then claim unbiased performance on that same set.
6. EDA: show counts before/after screening, source/date coverage, text completeness, platform-specific skill-reporting **shares** among eligible posts with explicit denominators, and validation error cases. Reddit–Nowcoder contrasts reflect **source platforms**, not China-vs-rest-of-world causal or representative national differences.
7. A2 repository must include raw/cleaned data, Codebook, 150-item Gold Set, collection/cleaning/extraction/validation notebooks, README/data documentation, AI-use log; report ≤10 pages excluding cover. The report's key conclusions must be the group's own judgment supported by validated results.

## 6. Revision log — v0.2 → v1.0 (based on 40 Pilot records)

| Modification | Pilot evidence that prompted it | Practical effect |
|---|---|---|
| Sharpened **role eligibility** | N0082 back-end; N0195 LLM algorithms; N0189 game ops; N0280 data product; N0116 blended development/analysis; R0135 multiple roles | Prevents non-analyst interview content from inflating the skill comparison; uses `U` for true mixed roles. |
| Clarified **real interview** vs discussion/preparation | R0205 preparing for an interview; R0365 SEC data-quality post; R0348 work-related SaaS case | Requires an actual interview before tagging interview skills. |
| Separated **nonreport (`0`)** from **uncertainty (`U`)** for formal validation | User-requested conversion of all pilot skill `0`s to `U`; heavy use of truncated Nowcoder snippets | Pilot convention retained as historical; formal Gold Set distinguishes absent mention from genuinely unjudgeable text. |
| Refined **overlapping assessment categories** | N0171 ML project deep dive, SQL/sorting/abnormality case; N0137 A/B design; R0344 coding preparation vs assessed skills | Allows multiple justified `1`s without double-counting irrelevant preparation. |
| Clarified **round counts and format** | R0410 interviewer sequence; R0344 many employers; N0386 written test | Stops treating question numbers or multiple firms as single-firm rounds; recognizes written test without new field. |
| Documented **snippet/missing evidence** | Several Nowcoder search-preview records; 40-pilot workbook with user-modified `U`s | Makes missingness and validation limitations explicit; avoids manufacturing evidence. |
| Clarified **coding provenance** | Joint pilot with AI-assisted corrections, no independently preserved A/B results | Prevents falsely reporting inter-coder metrics for the 40 pilot. |

**No new research variable has been introduced in v1.0.** The changes are definitions, allowed values, exclusions, and reproducibility rules. The formal Gold Set remains to be independently created and validated.
