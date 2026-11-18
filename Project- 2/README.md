# Data Jobs Market Analysis (Excel)

## Overview

Job postings can reveal which skills employers want and what they pay for them. In this project I explored a real dataset of data-job listings to find out what separates higher-paying roles from lower-paying ones.

**Workbook:** [2_Project_Analysis.xlsx](Project_Analysis.xlsx)

## Questions I Set Out to Answer

1. Do roles that list more skills pay more?
2. How does salary change from region to region?
3. Which skills show up most often in data jobs?
4. What do the 10 most requested skills actually pay?

## Excel Skills Used

- **📊 PivotTables:** summarized thousands of postings by role, country and skill
- **📈 PivotCharts:** turned the summaries into visuals
- **🧮 DAX:** wrote measures for medians and conditional calculations
- **🔍 Power Query:** cleaned and reshaped the raw data
- **💪 Power Pivot:** linked tables together in a data model

## Data

A 2023 dataset of real data-job postings, provided through a guided Excel course. It covers:

- **👨‍💼 Job titles**
- **💰 Salaries**
- **📍 Locations**
- **🛠️ Skills**

---

## 1️⃣ Do more skills mean better pay?

### Preparing the data with Power Query

**Extract:** I pulled in the source file (`data_salary_all.xlsx`) and split it into two queries: one with the full job details, and one listing the skills attached to each job ID.

**Transform:** For both queries I fixed column data types, dropped columns I didn't need, removed unwanted words from text fields and trimmed extra spaces.



![Jobs query](/Images/Project_Analysis/2_Project_Analysis_Screenshot1.png)




![Skills query](/Images/Project-2/2_Project_Analysis_Screenshot2.png)



**Load:** I loaded both cleaned queries into the workbook as tables (`data_jobs_all` and `data_job_skills`) to use in the rest of the analysis.



![Jobs table](/Images/Project-2/2_Project_Analysis_Screenshot3.png)




![Skills table](/Images/Project-2/2_Project_Analysis_Screenshot4.png)



### Findings

- Median pay tends to rise as the number of listed skills rises, most clearly for Senior Data Engineer and Data Scientist roles.
- Roles that ask for fewer skills, such as Business Analyst, sit at the lower end of the pay range.



![Skills vs salary](/Images/Project-2/2_Project_Analysis_Chart1.png)



**Why it matters:** Building a broader set of in-demand skills is a practical way to move toward higher-paying roles.

---

## 2️⃣ How does salary vary by region?

### PivotTable and DAX

I built a PivotTable on top of the data model, with `job_title_short` in the rows and `salary_year_avg` in the values. Then I wrote DAX measures to calculate median pay.

A general median measure:

```
Median Salary := MEDIAN(data_jobs_all[salary_year_avg])
```

A measure limited to US postings:

```
US Median Salary :=
CALCULATE(
    MEDIAN(data_jobs_all[salary_year_avg]),
    data_jobs_all[job_country] = "United States"
)
```

### Findings

- Senior Data Engineer and Data Scientist roles pay the most both inside and outside the US.
- The US-versus-international gap is widest for high-tech roles, which likely reflects how many tech companies are based in the US.



![Salary by region](/Images/Project-2/2_Project_Analysis_Chart2.png)



**Why it matters:** Knowing regional pay levels helps both candidates and employers set realistic salary expectations.

---

## 3️⃣ Which skills are most in demand?

### Building the data model with Power Pivot

I added both cleaned tables to one data model and linked them through the `job_id` column. Because Power Query had already cleaned the data, the relationship worked without extra fixes. The Power Pivot window also made it easier to refine the model and create measures.



![Data model](/Images/Project-2/2_Project_Analysis_Screenshot5.png)




![Power Pivot window](/Images/Project-2/2_Project_Analysis_Screenshot6.png)



### Findings

- SQL and Python lead the list, which shows how central they are to working with data.
- AWS and Azure also appear often, pointing to growing demand for cloud skills.



![Top skills](/Images/Project-2/2_Project_Analysis_Chart3.png)



**Why it matters:** The most requested skills are a good guide for what to learn next.

---

## 4️⃣ What do the top 10 skills pay?

### Combo PivotChart

I built a combo chart from a PivotTable that compares pay and demand for each skill:

- **Primary axis:** median salary, as clustered columns
- **Secondary axis:** how often the skill appears in postings (%), as a line with markers

I added titles, hid the connecting line and changed the markers to diamonds.

### Findings

- Python, Oracle and SQL are linked with the higher median salaries.
- PowerPoint and Word have the lowest pay and appear least often among high-paying roles.



![Top 10 skills pay](/Images/Project-2/2_Project_Analysis_Chart4.png)



**Why it matters:** Time spent learning skills like Python and SQL is more likely to raise earnings than general office tools.

---

## Skills Gained

- Cleaning and reshaping messy data with Power Query
- Linking tables and writing DAX measures in Power Pivot
- Summarizing large datasets with PivotTables and PivotCharts
- Combining salary and demand in one combo chart
- Turning analysis into clear takeaways

## Conclusion

This project used Excel's data tools to look at the data job market from several angles: skill count, region, demand and pay. The clearest pattern was that broader skill sets and skills like Python, SQL and cloud platforms go with higher pay. I hope it gives other job seekers a useful starting point for deciding what to learn.

## Credits

Built as a guided project from Luke Barousse's Excel course.
