# Top DS Skills Analysis
## 1.Project Summary
### <ins>Summary</ins>:
Over the past few years, jobs and interest in data science, AI and machine learning have risen exponentially. With COVID-19, data and technology has evolved tremendously. Due to its increasing demand and as students of MADS. We aim to understand more about the job market.

Through analyzing the job descriptions of two leading recruiting websites: Glassdoor and Indeed, we aim to understand:
- What data science skills are in hot demand in the job markets since that 
  - Implies the trend of data science, and 
  - Indicates the direction of study and work for data science practitioners as well as 
  - Assists to measure the value of data science practitioners. 

The following questions will guide us throughout this project:
  1) What are the top 10 hottest skills for data science in the job market? How did those skills evolve over a specific time period and distributed by countries, industries?
  2) What differences are there in skill requirements between data scientists and other jobs related to data such as data analyst, business analyst, data engineer, etc?

## 2. Datasets

2 datasets are used in this project, both come from the datasets of kaggle. 

<b>1st dataset</b>:
- Short description: Glassdoor’s posted job info, the following 6 columns are extracted for the further analysis, which includes:

| Column Names | Column Descriptions |
| :----------- | :----------------- |
| job.discoverDate | job posting date | 
| job.description | job posting description |
| header.jobTitle | job title |
| header.location | job location |
| header.employerName | employer name |
| gaTrackerData.industry | industry |


- Estimated size: 915 MB
- Location: https://www.kaggle.com/datasets/andresionek/data-jobs-listings-glassdoor?select=glassdoor.csv
- Format: CSV
- Access method: Download

<b>2nd dataset</b>:
- Short description: Indeed’s posted job info, the following 6 columns are extracted for the further analysis, which includes:

| Column Names | Column Descriptions |
| :----------- | :----------------- |
| Crawl Timestamp | job posting date | 
| Job Description | job posting description |
| Job Title | job title |
| Location | job location |
| Company Name | employer name |
| Industry | industry |

- Estimated size: 153 MB
- Location: https://www.kaggle.com/datasets/promptcloud/indeed-job-posting-dataset
- Format: CSV file.
- Access method: Download

## 3. Cleaning and manipulation
The whole data preprocessing includes the following stages:
- <b><ins>Filtration</b></ins>:
  - Filter non-data related jobs from both datasets.
- <b><ins>Standardization</b></ins>:
  - Standardize the names and descriptions of country, industry, employer name.
  - Standardize the format of job posting date.
- <b><ins>Filling missing data</b></ins>:
  - Fill missing industries for the 1st dataset.
  - Assign industries for the 2nd dataset
- <b><ins>Key phrases extraction</b></ins>:
  - Convert the html format to the text for the job description.
  - Extract skills from the converted job description by key phrase extraction, regular expression or other methods.
- <b><ins>Merging</b></ins>:
  - Remove duplicate records if the job posting records are from the same employer, the content and titles are similar.

The key challenges that we expect to encounter are the following:
- Extracting the skills from the text since no pattern and standards are available to search and extract those terms, which may consist of single or multiple words in addition to some terms that look different, but those implying the same skills such as coding vs. programming.
- Given the 2nd dataset does not include industries, it may require to fill this feature by other ways such as finding out the industries based on employer names from the 1st dataset given it has industries, or predict the industries based on the key words of employer names in the 2nd dataset.
- Remove duplicate job posting records given employer names, content and tiles, especially since the content includes lots of text, so we need to evaluate the contents to verify whether or not they are the same.
