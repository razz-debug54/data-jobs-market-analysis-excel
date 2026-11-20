# 📐 DAX Measures & Formatting Documentation (`Project_Analysis.xlsx`)

## Data Model Overview
- **Fact / Core Table:** `data_jobs_salary` (Job postings, titles, countries, annual salaries)
- **Bridge / Dimension Table:** `data_jobs_skills` (Job ID to skill mapping: Python, SQL, AWS, Azure, Excel, Tableau, Power BI, Spark, Snowflake, etc.)
- **Relationship:** `data_jobs_salary[job_id]` (`1`) $\rightarrow$ `data_jobs_skills[job_id]` (`*`)

---

## Measures Reference

| Measure Name | Table | DAX Formula | Number Format |
| :--- | :--- | :--- | :--- |
| **Job Count** | `data_jobs_salary` | `=DISTINCTCOUNT(data_jobs_salary[job_id])` | `#,##0` |
| **Skills Count** | `data_jobs_skills` | `=COUNT(data_jobs_skills[job_skills])` | `#,##0` |
| **Skills per job avg** | `data_jobs_skills` | `=DIVIDE([Skills Count], [Job Count])` | `0.00` |
| **Skill - likelihood** | `data_jobs_skills` | `=DIVIDE([Skills Count], CALCULATE([Job Count], ALL(data_jobs_skills[job_skills])))` | `0.0%` |
| **Median Salary** | `data_jobs_salary` | `=MEDIAN(data_jobs_salary[salary_year_avg])` | `$0,"k"` |
| **US Median Salary** | `data_jobs_salary` | `=CALCULATE(MEDIAN(data_jobs_salary[salary_year_avg]), data_jobs_salary[job_country] = "United States")` | `$0,"k"` |
| **Non US Median Salary** | `data_jobs_salary` | `=CALCULATE(MEDIAN(data_jobs_salary[salary_year_avg]), data_jobs_salary[job_country] <> "United States")` | `$0,"k"` |
| **Median Salary - Skills** | `data_jobs_skills` | `=MEDIAN(data_jobs_salary[salary_year_avg])` | `$0,"k"` |
