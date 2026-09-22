# MGS-4701-W01
Data and documentation for Group2(Wonder4): what actually happens in a BA/DA/analytics interview in 2026.

Introduction of Group2(Wonder4):

## Track 3: What Actually Happens in a BA/DA Interview (2026)
### What the data are
#### Reddit
The Reddit dataset consists of public Reddit posts discussing BA, DA, analytics internship, and related interview experiences. The dataset includes post titles, post text, publication dates, scores, URLs, and the search keyword used to retrieve each post.

#### Nowcoder
The Nowcoder dataset consists of public, self-reported interview-related posts returned by the Nowcoder search interface. The current pilot uses two search queries: `数据分析面经` (Data Analyst Interview Experiences) and `商业分析面经` (Business Analyst Interview Experiences). The extracted data include the search query, search-result page and rank, post type, post ID and UUID, title, post content, author information, publication time, source URL, and a deduplication key. For the `数据分析面经` query, pages 1–20 produced 400 raw search records. After deduplication, 380 unique posts remained, and 275 were identified as preliminary BA/DA/analytics interview candidates. The relevance flag is used only for preliminary screening and is not treated as a final validated label.

### Where they came from
#### Reddit

#### Nowcoder
The data came from the publicly accessible search interface of Nowcoder (牛客网). Nowcoder's search API was not directly called by our Python code. Instead, the search terms were entered manually in a normal browser session, and search-result pages were manually navigated while Chrome Developer Tools → Network recorded the data loaded by the browser. The Network logs were then exported as HAR files. Python was used only to read the locally saved HAR files, locate the stored search-result data, extract post-level records, and export them into structured CSV files.

### When they were collected
#### Reddit

#### Nowcoder
The current Nowcoder pilot data were collected in September 2026. For each search query, up to 20 pages of search results were manually navigated and captured through the browser Network panel. The raw datasets retain historical posts returned by the Nowcoder search interface. For the main analysis, records will later be restricted to the selected analysis time window so that the Nowcoder and Reddit samples can be compared consistently.

### How to reproduce the pilot
#### Reddit

#### Nowcoder
To reproduce the Nowcoder pilot:
1. Open Nowcoder in a normal browser session.
2. Search one of the predefined queries, such as `数据分析面经` or `商业分析面经`.
3. Open Chrome Developer Tools → Network.
4. Manually navigate through the search-result pages.
5. Export the captured Network log as a `.har` file.
6. Place the HAR file in the notebook directory or the designated `raw_har/` folder.
7. Open the corresponding Jupyter notebook and specify the HAR filename and expected search query.
8. Run the notebook from top to bottom.
9. Check the page-coverage output and exported CSV files.
The processing pipeline is:
`Browser search → HAR export → Python reads HAR → extract stored search-result records → audit page coverage → deduplicate posts → preliminary relevance screening → export CSV`
The notebook processes the saved HAR file offline and does not send new requests to the Nowcoder search API.

### Repository structure
#### Reddit

#### Nowcoder
The Nowcoder component currently contains two Jupyter notebooks and two query-specific CSV datasets:
- `nowcoder_数据分析面经_FULL20_REPRODUCIBLE_PIPELINE_V3.ipynb`
- `nowcoder_HAR_FULL20_REPRODUCIBLE_PIPELINE_V2.ipynb`
- `nowcoder_数据分析面经数据.csv`
- `nowcoder_商业分析面经数据.csv`
The notebooks contain the HAR parsing, record extraction, page-coverage checking, deduplication, and preliminary relevance-screening procedures used to produce the structured datasets.

### Sampling note
#### Reddit

#### Nowcoder
The Nowcoder dataset is not a random sample of all BA/DA interviews. The records included in the pilot depend on the selected search terms, Nowcoder's search and ranking system, the interview experiences that users choose to share publicly, and the availability of historical posts. The same post may also appear in more than one search query. Duplicate records are therefore removed using stable identifiers, primarily UUID and content ID. A keyword-based rule is used for preliminary relevance screening. A post is marked as a candidate when its title or content contains at least one BA/DA/analytics-related role term and at least one interview-related term. This automated screening may contain false positives or miss relevant posts, so it will be followed by manual validation before the final analysis.
