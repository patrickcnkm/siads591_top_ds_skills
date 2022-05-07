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

<b>Processing steps</b>:
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


<b>Expected output</b>:

After the data cleaning and manipulation, the expected output as below:

<ins>Table 1</ins>: Main table
- Name: main
- Description: the table stores the processed job detail info.
- Format: Pandas Dataframe
- Fields:

| Names | Descriptions | Data Type | Format | Constraints |
| :----------- | :----------------- | :----------------- | :----------------- | :----------------- |
| posting_date | Job posting date | Datetime | MM-DD-YYYY | Not null |
| description | Job posting description | String | In English, lowercase | Not null |
| title | job title | String ( 80 characters) | In English, lowercase |  |
| country | country of job | String ( 80 characters) |  In English, lowercase,full name of country |  |
| employer | Employer full name | String ( 80 characters) | In English, lowercase | Not null  |
| industry | Industry name | String ( 80 characters) | In English, lowercase (to be listed) |  |
| id  | Unique id to identify job posting, automatically generated during data manipulation process | int64 | 11 digits | Unique, foreign key to the table ( skill) |
| source | From Glassdoor or Indeed |  String |  ‘Glassdoor’ ‘Indeed’ |  Not null |

<ins>Table 2</ins>: Skill table
- Name: skills
- Description: the table stores the skill from each job posting.
- Format: Pandas Dataframe
- Fields:

| Names | Descriptions | Data Type | Format | Constraints |
| :----------- | :----------------- | :----------------- | :----------------- | :----------------- |
| id | Unique id to identify job posting, automatically generated during data manipulation process | int64 | 11 digits | Unique, foreign key to the table ( main) |
| skill | Skill name | String |  | Not null  |
| type | Skill type | String | ‘Soft skills’, such as leadership, teamwork etc. ‘Hard skills’, such as python programming, supervised learning algorithms etc. | Not null |

 ## 4. Analysis
 
 <b>Analysis flow</b>

- <b><ins>Identify the top skills for data-related positions</b></ins>:
  - <b>Approach</b>: Parse the skills from the job description from the combined dataset using Spark and group by positions then visualize the resulting manipulation.
  - <b>Expectation</b>: Many data related jobs will have similar skills, but for each position certain skills will be emphasized, highlighted, or weighted more than other positions.

- <b><ins>Distribution of skills across industries, countries, and time periods</b></ins>:
  - <b>Approach</b>: Using Pandas and Numpy to manipulate the data to plot different distributions of skill requirements across industries, countries and time periods.
  - <b>Expectation</b>: The progression of big data, AI, and machine learning varies for each country while different combinations of skills will be required for various industries. For example, the expectations and requirements for a job in the United States will differ from those of a job in Hong Kong.

- <b><ins>Characteristics of data-related jobs</b></ins>:
  - <b>Approach</b>: Using K-means clustering/topic modeling to group and analyze the data-related skill requirements.
  - <b>Expectation</b>: In different industries, we expect to see specific skills standout as well as different countries/locations.

## 5. Visualization
- <b><ins>Bar Chart</b></ins>: To analyze the top 10 skills in the job markets, which can be further broken down by industries (in the 1st subplot in bar chart), countries (in the 2nd subplot in heatmap)
- <b><ins>Line Chart</b></ins>: To analyze the trend of DS skills over the span of one year.
Features include DS skills on the y-axis and date on the x-axis
- <b><ins>Stacked Bar Chart</b></ins>: To analyze the differences between required skills for data science jobs and non-data scientist jobs.
- <b><ins>Scatterplot</b></ins>: To visualize and analyze the results from clustering.

## 6. Ethical Consideration
- <b><ins>Bias from the judgment of DS skills</b></ins>. Defining and categorizing skills may be impacted by the bias from project members given human judgment is required here. The final analysis could mislead the audience, for example, some skills are excluded but those may be counted as one of top 10. To mitigate the risk, we may consider introducing the 3rd party tools to validate the definition and category of skills.

- <b><ins>Transparency on potential algorithms used to extract DS skills</b></ins>. Algorithms may be introduced to extract key phrases in terms of DS skills. How those algorithms work, and what key factors may impact the results will be explained and presented in the related project documents to provide a more in depth explanation, which could improve the transparency of algorithms and win the trust of users or audiences.
