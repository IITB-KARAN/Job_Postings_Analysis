# SQL Data Analyst Job Market Analysis

## Project Overview

This project explores the 2023 data analyst job market using SQL to uncover salary trends, identify the most in-demand skills, and determine which technical skills offer the highest earning potential. The analysis is based on real-world job posting data and provides practical insights for aspiring data analysts looking to make informed career decisions.

**SQL Queries:**All queries used throughout this project are available in here [Queries](/Job_Postings_Analysis/1_SQL_Analysis/SQL_Queries)



---

# Background

Choosing the right technical skills can significantly impact career growth in data analytics. This project was developed to analyze the current job market and answer questions such as:

- Which data analyst positions offer the highest salaries?
- What skills are required for those high-paying roles?
- Which technical skills are most frequently requested by employers?
- Which skills command the highest salaries?
- What skills provide the best balance between market demand and earning potential?

The dataset originates from Luke Barousse's SQL course and contains information about job titles, salaries, companies, locations, and required technical skills.

---

# Tech Stack

This project was completed using the following technologies:

- **SQL** – Data extraction and analysis
- **PostgreSQL** – Database management system
- **Visual Studio Code** – SQL development environment
- **Git & GitHub** – Version control and project hosting

---

# Project Analysis

## 1. Top-Paying Data Analyst Jobs

The first analysis identifies the highest-paying remote data analyst positions by filtering jobs with available salary information.

```sql
SELECT
         job_id,
         job_title,
         job_location,
         job_schedule_type,
         salary_year_avg,
         job_posted_date,
         name AS company_name
FROM 
        job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id        
WHERE
        job_title_short = 'Data Analyst' AND 
        job_location = 'Anywhere' AND
        salary_year_avg IS NOT NULL
ORDER BY 
        salary_year_avg  DESC
LIMIT 10;  
```

### Key Findings

- Annual salaries ranged from **$184,000 to $650,000**.
- Top-paying opportunities were offered by companies across multiple industries.
- Senior-level and leadership positions consistently commanded the highest salaries.

![Top Paying Roles](images/1_top_paying_roles.png)

---

## 2. Skills Required for Top-Paying Jobs

This analysis identifies the technical skills associated with the highest-paying data analyst positions by combining job postings with their required skills.

```sql
SELECT
         job_id,
         job_title,
         job_location,
         job_schedule_type,
         salary_year_avg,
         job_posted_date,
         name AS company_name
FROM 
        job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id        
WHERE
        job_title_short = 'Data Analyst' AND 
        job_location = 'Anywhere' AND
        salary_year_avg IS NOT NULL
ORDER BY 
        salary_year_avg  DESC
LIMIT 10;  
```

### Key Findings

- **SQL** appeared most frequently among top-paying positions.
- **Python** was the second most requested skill.
- **Tableau**, **R**, **Snowflake**, **Excel**, and **Pandas** were also common requirements.

![Top Paying Skills](images/2_top_paying_roles_skills.png)

---

## 3. Most In-Demand Skills

The following query determines which technical skills appear most frequently across remote data analyst job postings.

```sql
SELECT
       skills_dim.skills,
       COUNT(skills_job_dim.job_id ) AS demand_count 
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE 
        job_title_short = 'Data Analyst' AND 
        job_location = 'Anywhere'
GROUP BY
        skills_dim.skills
ORDER BY
        demand_count DESC
LIMIT 5;                    
```

### Most Requested Skills

| Skill | Demand |
|--------|--------:|
| SQL | 7,291 |
| Excel | 4,611 |
| Python | 4,330 |
| Tableau | 3,745 |
| Power BI | 2,609 |

### Insights

- SQL remains the core skill for data analysts.
- Excel continues to be an essential business tool.
- Python is increasingly important for data processing and automation.
- Tableau and Power BI dominate the visualization landscape.

---

## 4. Highest-Paying Skills

This analysis examines the average salary associated with individual technical skills.

```sql
SELECT 
    skills,
    ROUND(AVG(salary_year_avg), 0) as avg_salary
FROM job_postings_fact

INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE 
    job_title_short = 'Data Analyst' AND
    salary_year_avg IS NOT NULL
GROUP BY 
    skills
ORDER BY
    avg_salary DESC
LIMIT 25;
```

### Top Paying Skills

| Skill | Average Salary |
|--------|---------------:|
| PySpark | $208,172 |
| Bitbucket | $189,155 |
| Couchbase | $160,515 |
| Watson | $160,515 |
| DataRobot | $155,486 |
| GitLab | $154,500 |
| Swift | $153,750 |
| Jupyter | $152,777 |
| Pandas | $151,821 |
| Elasticsearch | $145,000 |

### Insights

- Big data technologies command premium salaries.
- Cloud platforms and modern data engineering tools continue to grow in value.
- Machine learning and automation skills significantly increase earning potential.

---

## 5. Most Valuable Skills to Learn

This query combines salary and demand data to identify skills that offer the strongest return on investment for aspiring data analysts.

```sql

SELECT
     skills_dim.skill_id,
    skills_dim.skills,
    COUNT(skills_job_dim.job_id) AS demand_count,
    ROUND(AVG(job_postings_fact.salary_year_avg),0) AS avg_salary 
FROM job_postings_fact

INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE 
        job_title_short = 'Data Analyst' AND
        salary_year_avg IS NOT NULL AND
        job_work_from_home = TRUE
GROUP BY 
        skills_dim.skill_id
HAVING
    COUNT(skills_job_dim.job_id) >10
ORDER BY
        demand_count DESC,
        avg_salary DESC
LIMIT 25;   
```

### Top Skills

| Skill | Demand | Average Salary |
|--------|--------:|---------------:|
| Go | 27 | $115,320 |
| Confluence | 11 | $114,210 |
| Hadoop | 22 | $113,193 |
| Snowflake | 37 | $112,948 |
| Azure | 34 | $111,225 |
| BigQuery | 13 | $109,654 |
| AWS | 32 | $108,317 |
| Java | 17 | $106,906 |
| SSIS | 12 | $106,683 |
| Jira | 20 | $104,918 |

### Insights

- Cloud platforms continue to dominate the modern analytics landscape.
- Big data technologies provide strong salary potential.
- SQL, Python, Tableau, and cloud tools remain excellent long-term investments for career growth.

---

# Skills Demonstrated

Throughout this project, I strengthened several practical SQL and data analysis skills, including:

- Writing complex SQL queries
- Using Common Table Expressions (CTEs)
- Performing multi-table joins
- Aggregating and summarizing data
- Ranking and filtering datasets
- Converting business questions into SQL solutions
- Interpreting analytical results for business decision-making

---

# Key Takeaways

The analysis highlights several important trends within the data analyst job market:

- Remote data analyst positions can offer salaries exceeding **$650,000**.
- SQL is both the most requested and one of the most valuable technical skills.
- Python, Tableau, and cloud technologies continue to grow in demand.
- Specialized technical skills often lead to higher salaries.
- Combining high-demand skills with high-paying technologies provides the best long-term career opportunities.

---

# Conclusion

This project demonstrates how SQL can be used to transform raw job posting data into meaningful career insights. By analyzing salary trends, employer requirements, and skill demand, the project provides a data-driven perspective on the current data analyst job market.

The findings can help aspiring data analysts prioritize learning paths, develop market-relevant technical skills, and make more informed career decisions.
