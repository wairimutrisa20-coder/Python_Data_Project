# The Analysis

## 1. What are the most demanded skill for the top 3 most popular data roles

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their topskills, showing which skills i should pay attention to depending on the role am targeting.

View my notebook with detailed steps here;
[2_Skills_Demand.ipynb](3_Projects\2_Skills_Demand.ipynb)

###Visualize Data

python

fig, ax = plt.subplots(len(job_titles), 1)
fig.set_size_inches(8, 12)

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)

    sns.barplot(data=df_plot, x= 'skill_percent', y= 'job_skills', ax=ax[i], hue= 'skill_count', palette= 'dark:b_r')

    
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].legend().set_visible(False)
    ax[i].set_xlim(0, 78)

    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n, f'{v:.0f}%', va= 'center')

#if i want to remove the number and leave on only the axis below

    if i != len(job_titles) - 1:
        ax[i].set_xticks([])

fig.suptitle('Counts of Top Skills in Job Postings')
fig.tight_layout(h_pad=0.5) #fix the overlap
plt.show()


#### Results

![Visualization of Top Skills for Data Nerds](3_Projects\IMAGES\skills_demand.png)

#### Insights

- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists(72%) and data Engineers(65%).
- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half the job postings for both roles. For Data Engineers, Python is the most sought-after skill, appearing in 68% of job postings.
- Data Engineers require more specialized technical skills(AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools(Excel, Tableau).

### How are in-demand skills trending for Data Analysts

Visualize Data
sns.set_theme(style='ticks')


# Select the top 6 skills
top_6_skills = df_DA_US_percent.max().nlargest(6).index

df_plot = df_DA_US_percent[top_6_skills]

# Create line plot
sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.despine(top=True, right=True)

plt.title('Monthly Trends of Top 6 Skills Required for Data Analyst Jobs')
plt.xlabel('Month (2023)')
plt.ylabel('Likelihood in Job Postings (%)')

# Remove the legend
plt.legend().remove()

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

# Label each line at its final data point
for i in range(6):
    plt.text(
        11.2,
        df_plot.iloc[-1, i],
        df_plot.columns[i]
    )

plt.tight_layout()
plt.show()

### Result
!Visualization(3_Projects\IMAGES\TrendSkills.png)

### Insights

SQL: SQL was the most demanded skill throughout 2023, although its demand gradually declined from approximately 63% in January to 53% in December. This highlights the importance of database querying and data management in Data Analytics.

Excel: Excel maintained strong demand, averaging around 40–45% for much of the year. This shows that spreadsheet skills remain essential for data manipulation, analysis and reporting.

Python: Python maintained relatively stable demand, ranging between approximately 30% and 36%. This demonstrates the importance of programming for data cleaning, automation and advanced analysis.

Tableau: Tableau experienced some fluctuations, with demand reaching approximately 33% in December. This suggests that data visualization remains an important skill for presenting analytical findings.

Power BI: Power BI maintained relatively consistent demand, mostly between 19% and 23%, highlighting the continued importance of business intelligence and dashboard development.

Overall trend: SQL, Excel and Python dominated the chart, while Tableau and Power BI remained relevant for visualization and reporting.