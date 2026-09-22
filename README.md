# MGS-4701-W01
Data and documentation for Group2(Wonder4): what actually happens in a BA/DA/analytics interview in 2026.

Introduction of Group2(Wonder4):

## Track 3: What Actually Happens in a BA/DA Interview (2026)

### Reddit Data
#### What the data are
The Reddit dataset consists of public Reddit posts related to BA, DA, and analytics internship interview experiences. The search also covers specific interview topics such as SQL interviews, case interviews, and the use of AI tools.
For each post, we collect:
- Search keyword
- Subreddit
- Post title
- Post text
- Publication date
- Reddit score
- Post URL

### Where they came from
The data were collected from two public Reddit communities:
- r/analytics
- r/datascience
The Reddit API was accessed through PRAW (Python Reddit API Wrapper).

### When they were collected
The pilot collection was conducted on September 22, 2026.
Posts published between January 1, 2023 and September 22, 2026 were included in the pilot collection.

### How to reproduce the pilot
1. Install the required Python packages: `praw`, `pandas`, and `python-dotenv`.
2. Set up Reddit API credentials and store them in a local `.env` file.
3. Open `reddit_data_collection.ipynb`.
4. Run the notebook from beginning to end.
5. The notebook searches r/analytics and r/datascience using the predefined keywords.
6. Posts outside the specified date range are excluded.
7. Duplicate posts are removed based on the post URL.
8. The final dataset is saved as `reddit_interview_pilot.csv`.
   
### Repository structure


### Sampling note
