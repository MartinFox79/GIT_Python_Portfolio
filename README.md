# DISCLAIMER

## Im currently working on this project, so this section might be still not finished but feel free to check it out



# The Analysis

## 1. What are the most demanded skills for the top 3 most  popular data roles?

To find the most in-demand skills in the data industry, I analyzed job postings to identify the top three most popular data roles. Then, I selected the five most common skills for each role. This shows which skills are most valuable for people who want to grow in these positions.

View my notebook with detailed steps here: [2_Skills_Demand.ipynb](Project/2_Skills_Demand.ipynb)

### Visualize Data

```python

fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data = df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue = 'skill_percent', palette='dark:b_r')
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].legend().remove()
    ax[i].set_xlim(0, 75)

    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v+1, n, f'{v:.0f}%', va='center')

    if i != len(job_titles) - 1:
        ax[i].set_xticks([])
fig.suptitle('Likelihood of Skills Requested in Poland Job Postings', fontsize=15)
fig.tight_layout()
plt.show()

```

### Results

![Visualization of Top Skills for Data Industry](Project/images/skill_demand_data_roles.png)

### Insights

#### General Conclusions
- Python and SQL are the two most important and universal skills across all data-related roles in Poland.
They appear as top requirements for Data Analysts, Data Engineers, and Data Scientists, showing that coding and database querying are essential in nearly every position.
- Cloud technologies (Azure, AWS) and data visualization tools (Tableau, Power BI) are becoming standard expectations, depending on the nature of the role.
- Each position emphasizes a slightly different skill mix — analysts focus on business tools, engineers on infrastructure, and scientists on modeling and analytics.

⸻

#### Data Analyst
- Core skills: SQL (50%) and Excel (37%) remain crucial for handling and preparing data.
- Python (30%) appears as a growing technical requirement, especially for automation and advanced analysis.
- Visualization tools like Tableau (22%) and Power BI (20%) highlight the importance of communicating insights effectively.

⸻

#### Data Engineer
- The role is dominated by Python (63%) and SQL (63%), emphasizing data pipeline and ETL development.
- Strong demand for Azure (41%), AWS (35%), and Spark (35%) reflects the shift toward cloud-based and distributed data systems.
- The skill set is clearly more technical and infrastructure-oriented compared to other roles.

⸻

#### Data Scientist
- Python (60%) and SQL (52%) are key foundational skills, showing overlap with engineering competencies.
- R (22%) is still relevant for statistical analysis and academic-style modeling.
- Azure (19%) and AWS (17%) suggest growing expectations for cloud-based machine learning deployment.



## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data

```python

plt.figure(figsize=(7,5))
sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style="ticks")
sns.despine()

plt.title('Trending Top Skills for Data Analysts in Poland')
plt.ylabel('Probability in Job Posting (%)')
plt.xlabel('2023')
plt.legend().remove()

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter())

palette = sns.color_palette('tab10')
offsets = [-2, 2, 5, -4, 7]

texts = []
for i, col in enumerate(df_plot.columns[:5]):
    x_pos = len(df_plot) - 1 
    y_pos = df_plot.iloc[-1, i]
    label_x = len(df_plot) + 0.5
    label_y = y_pos + offsets[i]

    # line connecting point to label
    plt.plot([x_pos, label_x], [y_pos, label_y],
        color=palette[i], lw=0.8, ls='--', alpha=0.7)

    texts.append(
        plt.text(
            label_x,
            label_y,
            col,
            fontsize=9,
            weight='bold',
            color=palette[i]
        )
    )

```
![Trending Top Skills for DA in Poland](Project/images/skill_trend_DA.png)

