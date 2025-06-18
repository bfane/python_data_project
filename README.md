## Overview
Welcome to my analysis of Data job Market, focusing on Data Analysts, Data Engineers, and Data Scientists roles. This project was created out of a desire to understand the Data job market better. It delves into the top-paying and in-demand to help find optimal job oppotunities for Data Analysts, Data Engineers, and Data Scientists. 

The data sourced from Luke Barousse which provides the foundation for my analysis. Through a series of Python scripts, I explore key questions such as the most demanded skills, salary trends, and the intersection of demand and salary in data analytics.

## The Questions

Below are the questions this project seeks to answer:

  1.What are the skills most in demand for the top 3 most popular data roles?

2. How are in-demand skills trending for Data Analysts?

3. How well do jobs and skills pay for Data Analysts?

4. What are the optimal skills for data analysts to learn?

## Tools

The following are the tools used:

Python: The backbone of my analysis, allowing me to analyze the data and find critical insights.
	
    - Pandas Library: The Pandas Library used to analyze the data.
	- Matplotlib Library: The library I used to visualize my Data.
	-Seaborn Library: The library I used to create advanced visuals.

Jupyter Notebooks: The tool I used to run my python scripts
Visual Studio Code: The tool for executing python scripts

Git & GitHub: Essential for version control and sharing my Python code and analysis, ensuring collaboration.

## Data Preparation and Data Cleaning

This section outlines the steps taken to prepare the data for analysis, ensuring accuracy and usability.

1. I imported the necessary Python libraries.
2. Loaded the dataset.
3. Initial Data Cleaning tasks to ensure Data quality.

## Filter US Jobs

To focus my analysis on the US job market,  I apply filters to the dataset, narrowing down to job roles based in the United States


# The Analysis


## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular roles, first we filtered the three most popular data roles, and then extracted the top 5 skills for those top 3 roles.
This query highlights the most popular job titles and their top skills.

View my notebook with detailed steps here:
[data_roles_skills.ipynb](Python_project\data_roles_skills.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles),1)

for i, job_title in enumerate(job_titles):
    df_plot2 = skill_job_perc[skill_job_perc['job_title_short']== job_title].head(5)
    #df_plot2.plot(kind='barh',y='skill_percent', x='job_skills',ax=ax[i],title=job_title)
    sns.barplot(data=df_plot2,y='job_skills',x='skill_percent',ax=ax[i],hue='skill_count',palette='dark:b_r')
    #ax[i].invert_yaxis()
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].legend().set_visible(False)
    ax[i].set_xlim(0,78)
    for n, v in enumerate(df_plot2['skill_percent']):
        ax[i].text(v +1 ,n, f'{v:.0f}%',va='center')
fig.suptitle('Likelihood of Skills in the US Job Postings', fontsize=13)
plt.tight_layout(h_pad=0.5)
```

### Results

![Visualization of Top Skills for Data Enthusiasts](Python_project\images\skill_demand_data_roles.png)


### Insights

- SQL is the most requested skill for Data Analysts and Data Scientists, with SQL in over half of the job postings for both roles. For Data Engineers, Python is the most sought after skill, appearing in 68% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more data management and data analysis tools (Excel, Tableau).
- Python is a versatile skill, highly demanded across all the three roles, but most prominently for Data Scientists (72%) and Data Engineers(65%).


## 2. How are in-demand skills trending for Data Analysts?

I first we filtered for Data Analysts that are in the US.Created a job posted month column that was used for the trend analysis.

This query highlights the most popular job skills for a Data Analyst in the United States aggregated on monthly basis.

View my notebook with detailed steps here:
[skills_trend.ipynb](Python_project\skills_trend.ipynb)


### Visualize Data

```python

sns.lineplot(data=df_plot,dashes=False,palette='tab10')
sns.set_theme(style='ticks')
sns.despine()
plt.title('Trending Top Skills for Data Analysts in the US')
plt.xlabel('2023')
plt.ylabel('Likelihood in Job Posting')
plt.legend().remove()

from matplotlib.ticker import PercentFormatter
ax =plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

for i in range(5):
    plt.text(11.3,df_plot.iloc[-1,i],df_plot.columns[i])
```

### Results

![Visualize Trending Top Skills for Data Analysts in the United States](Python_project\top_skills_da.png)

### Insights
- SQL remains the most demanded skill throughout the year followed by Excel for Data Analysts in the US.







