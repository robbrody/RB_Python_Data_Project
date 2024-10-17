# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

I started by filtering the jobs for US based jobs only. I found the most demanded skills for the top 3 most popular data roles, I filtered out those positions by the most popular, and got the top 5 skills for each of these top 3 roles. This query highlights the 3 most popular job titles and their associated top 5 skills, showing which skills I should pay attentin to depending on the data role I'm targeting.

View my notebook with detailed steps here:  
[2_Skill_Demand.ipynb](3_Project/2_Skill_Demand.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)

    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:teal_r')
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].set_title(job_title)
    ax[i].set_xlim(0, 78)
    ax[i].legend().set_visible(False)
    
    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n, f'{v:.0f}%', color='black', va='center')

    if i != len(job_titles) - 1:
        ax[i].set_xticks([])

fig.suptitle('Likelihood of Skills Requested in US Job Postings',fontsize=15)
fig.tight_layout()
plt.show()
```

### Results

![Visualization of Top Skills for Top Roles](3_Project/images/skill_demand_all_data_roles.png)

### Insights

- Python is a versaltile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%). 
- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half the job postings for both roles. For Data Engineers SQl is the most sought after skill appearing in 68% of Job Postings.
- Data Engineers require more specialized skills (AWS, Azure, SPark). Data Analysts need general business tools like Excel, and visualization in Tableau. Data Scientists roles are looking for Python, SQL, and R for more programming based analysis. 