# MGS4701_Wonder4_AS2
# BA/DA Interview Experience Analysis on Nowcoder

## Project Overview

This project analyzes interview experiences shared on Nowcoder, a Chinese career discussion platform, to identify frequently reported interview topics and question types in Business Analytics (BA) and Data Analytics (DA) roles.

Our refined research question is:

**Among the selected Nowcoder posts reporting BA/DA interview experiences, which interview topics and question types are most frequently reported, and what evidence is provided of assessments of AI-tool proficiency?**

The unit of analysis is an individual post. Each post may report multiple interview rounds and skill categories.

## Data Collection

The initial project collected candidate posts from Nowcoder and Reddit. Following a refinement of the research question, the final analysis focuses exclusively on Nowcoder.

The Nowcoder data were collected in September 2026 using two search keywords:

- 商业分析面经 (Business Analyst Interview Experiences)
- 数据分析面经 (Data Analyst Interview Experiences)

The initial search exports contained 795 records, with 743 unique posts after deduplication across the two searches.

The prepared classification dataset subsequently contained 944 records, including 394 Nowcoder posts and 550 Reddit posts. The intermediate selection from the original Nowcoder search results to these 394 candidates requires further documentation.

## Data Cleaning and Classification

The data processing workflow includes:

1. **Data Standardization:** Organize records into consistent fields, including title, text, date, URL, and platform.
2. **Data Quality Checks:** Examine duplicate identifiers and URLs, missing fields, and text completeness.
3. **Gold Set Labeling:** Use 150 labeled posts to establish reference classifications.
4. **Supervised Model Training:** Train text classifiers to identify relevant interview posts and interview skill categories.
5. **Automated Classification:** Apply trained models to the remaining 794 candidate posts.
6. **Nowcoder Filtering:** Retain Nowcoder posts classified as `include`.
7. **Quality Review:** Flag predictions and ambiguous records requiring further human verification.

The preliminary cleaned dataset contains **387 Nowcoder posts**, including 68 records with supplied reference labels and 319 records classified by the supervised model.

## Key Variables

The analysis includes ten interview topic and skill indicators:

`sql`, `programming`, `statistics`, `machine_learning`, `business_case`, `product_metrics`, `bi_visualization`, `behavioral`, `project_experience`, and `ai_tool_assessment`.

Additional variables describe interview rounds, assessment formats, and publication dates.

Skill categories are not mutually exclusive. A missing or unreported skill does not necessarily mean that the skill was absent from the actual interview.

## Exploratory Data Analysis

Among the 387 selected Nowcoder posts, the most frequently positively coded categories are:

| Interview Category | Posts | Percentage |
|---|---:|---:|
| Project Experience | 228 | 58.9% |
| Business Case | 160 | 41.3% |
| Behavioral | 84 | 21.7% |

For AI-tool assessment, two posts were positively labeled, while 319 records were classified as unknown. This limits conclusions about how frequently AI-tool proficiency is assessed.

These results describe reported content under the existing labels, rather than validated frequencies across all BA/DA interviews.

## Validation and Limitations

The current dataset is preliminary. Of the 387 retained posts, 319 were classified automatically and have not all been independently verified.

Five-fold cross-validation produced approximately 86% relevance accuracy, but a simple platform-based baseline achieved a similar result. Therefore, this metric alone does not establish reliable classification performance.

Further limitations include incomplete post excerpts, search-based sampling, and uncertainty in some skill labels. The dataset should not be treated as fully human-validated until the relevant records have been reviewed.

## Reproducibility

The data processing workflow is documented in:

`01_Nowcoder_Data_Cleaning_and_Classification.ipynb`

Required input files:

- `raw data.csv`
- `Goldset.csv`

The Notebook trains the classification models, generates validation diagnostics, predicts relevance labels, and exports the preliminary Nowcoder dataset.

The original HAR-based data collection is a separate process and is not reproduced by this classification Notebook.
