# Introduction
 
An end-to-end data analysis project examining the 2023–2024 data job market, executed across three distinct tools — **SQL, Excel, and Power BI** — to answer one central question:
 
> **For a career in data, which skills are worth learning, and what do they pay?**
 
##  Project Overview
 
Career guidance in the data field is often generic and anecdotal. This project takes a data-driven approach instead, analyzing thousands of real job postings to determine:
 
- Which roles command the highest salaries, and who is hiring for them
- Which skills employers most frequently require
- Which skills offer the strongest return — a balance of high demand and high salary
- How factors such as location and specialization influence compensation
The project was carried out as a full analytical pipeline: sourcing and structuring the data, querying it with SQL, building dashboards in Excel, and delivering interactive reporting in Power BI. The same core dataset and questions were addressed through each tool to demonstrate consistent analytical reasoning applied across different environments.
 
##  Key Findings
 
- **SQL is the most valuable skill in the dataset** — it ranks highest in both demand and its association with top-paying roles.
- **The strongest combination is SQL, Python, and a visualization tool** (Tableau, Excel, or Power BI). This pairing recurs consistently across all three analyses.
- **Specialized and big-data skills command a premium.** Tools such as PySpark, Bitbucket, Couchbase, Snowflake, and cloud platforms (AWS, Azure) yield the highest average salaries despite comparatively lower demand.
- **Salary tends to increase with the number of required skills**, particularly for Senior Data Engineer and Data Scientist roles.
- **Location remains a significant factor, even for remote positions.** Compensation varies meaningfully by country, and the highest-paying remote roles ($180K–$650K) are concentrated in senior and leadership positions.
- **Excel remains highly relevant.** It is the second most in-demand skill after SQL, underscoring its continued importance in employer expectations.
##  Project Structure
 
| Stage | Tool | Description |
|---|---|---|
| [`1_SQL_Analysis`](./1_SQL_Analysis) | PostgreSQL, VS Code | SQL queries identifying top-paying jobs, the skills associated with those jobs, the most in-demand skills, the highest-paying skills, and the optimal skills (balancing demand and salary) |
| [`2_Excel_Dashboard`](./2_Excel_Dashboard) | Excel (Power Query, Power Pivot, DAX, PivotTables) | Two interactive dashboards: a salary exploration tool, and a 2.0 version analyzing the relationship between skills, salary, and regional pay differences |
| [`3_Powera_BI_Dashboard`](./3_Powera_BI_Dashboard) | Power BI | Two `.pbix` dashboards featuring drill-through pages, KPI cards, and geospatial visualizations of job postings |
 
Each stage of the pipeline includes its own README with the complete methodology — queries, dashboards, and tool-specific insights.
 
## Tools & Technologies
 
- **PostgreSQL**
 - **SQL**
 - **VS Code**
 - **Microsoft Excel (Power Query,Power Pivot, DAX)**
- **Power BI**
 - **Git & GitHub**