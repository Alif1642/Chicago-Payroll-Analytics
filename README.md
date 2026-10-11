# Chicago Payroll Analytics-

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![pandas](https://img.shields.io/badge/pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Dataset](https://img.shields.io/badge/Data-City%20of%20Chicago-0B5394)](https://data.cityofchicago.org/Administration-Finance/Current-Employee-Names-Salaries-and-Position-Title/xzkq-xp2w)

An exploratory data analysis project examining employee roles, departments, work status, annual salaries, hourly rates, and typical working hours in a City of Chicago payroll dataset. The analysis uses Python and pandas to answer a structured set of workforce and compensation questions in a reproducible Jupyter Notebook.

## Project Overview

The project demonstrates a practical tabular-data workflow:

- loading and inspecting a public payroll dataset;
- assessing data types, missing values, and descriptive statistics;
- cleaning currency-formatted salary and hourly-rate fields;
- filtering records with multiple conditions;
- grouping and aggregating data by department and payment type;
- identifying workforce and compensation patterns;
- exporting the transformed dataframe for further analysis.

The repository is intentionally notebook-focused. It does not currently include a dashboard, production application, or predictive model.

## Dataset

The included CSV is a snapshot of the City of Chicago employee payroll data. The official data portal describes whether employees are paid by salary or hourly rate and provides typical hours for hourly employees.

- **Source:** [City of Chicago Data Portal](https://data.cityofchicago.org/Administration-Finance/Current-Employee-Names-Salaries-and-Position-Title/xzkq-xp2w)
- **Local file:** `City_of_Chicago_Payroll_Data.csv`
- **Rows:** 32,658
- **Source columns:** 8
- **Departments:** 36
- **Unique job titles:** 1,095
- **Unique employee names:** 32,350

> The findings in this repository describe the included CSV snapshot. The live City of Chicago dataset may change over time.

### Data Dictionary

| Column | Description |
|---|---|
| `Name` | Employee name as recorded in the source data |
| `Job Titles` | Employee position title |
| `Department` | City department or administrative unit |
| `Full or Part-Time` | Full-time (`F`) or part-time (`P`) indicator |
| `Salary or Hourly` | Indicates whether compensation is salary-based or hourly |
| `Typical Hours` | Typical weekly hours for hourly employees |
| `Annual Salary` | Annual salary stored as a currency-formatted string |
| `Hourly Rate` | Hourly rate stored as a currency-formatted string |

The notebook derives two additional numeric fields:

- `Salary` from `Annual Salary`;
- `H_Rate` from `Hourly Rate`.

## Analysis Questions

The notebook answers 24 practical questions, including:

1. What is the shape and structure of the dataset?
2. How many missing values are present in each column?
3. How many employees are salaried versus hourly?
4. Which department has the largest workforce?
5. How are salaried and hourly employees distributed within the Police department?
6. What are the minimum, maximum, and average annual salaries?
7. Who has the maximum annual salary in the included snapshot?
8. What are the minimum, maximum, and average hourly rates?
9. How many hourly employees earn below the average hourly rate?
10. How many hourly employees are full-time?
11. How many unique job titles appear in the data?
12. What is the average salary by department?
13. Which job title is most common?
14. How many job titles contain the word `officer`?

## Key Findings

| Metric | Result |
|---|---:|
| Total payroll records | 32,658 |
| Salaried records | 24,775 |
| Hourly records | 7,883 |
| Full-time records | 30,676 |
| Part-time records | 1,982 |
| Largest department | Police - 12,973 records |
| Most common job title | Police Officer - 9,393 records |
| Average annual salary | $87,512.78 |
| Median annual salary | $90,024.00 |
| Maximum annual salary | $300,000.00 |
| Average hourly rate | $32.87 |
| Median hourly rate | $35.60 |
| Maximum hourly rate | $96.00 |
| Average typical hours | 34.70 hours |
| Full-time hourly records | 5,906 |
| Job titles containing `officer` | 11,101 records |

### Department Distribution

The five departments with the most records are:

| Rank | Department | Records |
|---:|---|---:|
| 1 | Police | 12,973 |
| 2 | Fire | 4,800 |
| 3 | Streets & Sanitation | 2,194 |
| 4 | Office of Emergency Management and Communications | 2,044 |
| 5 | Water Management | 1,878 |

### Compensation Observations

- The notebook identifies the maximum annual salary as **$300,000** for the **Commissioner of Aviation** in the included snapshot.
- The maximum hourly rate is **$96.00** for a **Psychiatrist** in the Health department.
- **2,791** hourly records fall below the dataset's average hourly rate.
- The Police department contains **12,941 salaried** and **32 hourly** records.
- An annual salary value of **$0.96** appears as the minimum. This should be treated as a potential data-quality anomaly and validated against the source before interpretation.

## Missing-Value Pattern

The source uses separate compensation fields for salaried and hourly employees, so the missing values are structurally meaningful:

| Column | Missing values |
|---|---:|
| `Typical Hours` | 24,775 |
| `Annual Salary` | 7,883 |
| `Hourly Rate` | 24,775 |

Salaried records generally contain `Annual Salary`, while hourly records contain `Typical Hours` and `Hourly Rate`.

## Tools and Techniques

- **Python** - analysis language
- **pandas** - loading, cleaning, filtering, aggregation, and export
- **Jupyter Notebook** - interactive analysis and documentation
- **CSV** - source and output data format

Techniques demonstrated:

- dataframe inspection with `head()`, `info()`, and `describe()`;
- null-value analysis with `isnull()`;
- currency-string conversion to numeric values;
- Boolean filtering with multiple conditions;
- `groupby()` aggregation and `value_counts()`;
- `idxmax()` and `idxmin()` record retrieval;
- text matching with `apply()` and a custom function;
- CSV export with `to_csv()`.

## Repository Structure

```text
Chicago-Payroll-Analytics/
├── Chicago_Payroll_Analysis.ipynb
├── City_of_Chicago_Payroll_Data.csv
└── README.md
```

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Alif1642/Chicago-Payroll-Analytics.git
cd Chicago-Payroll-Analytics
```

### 2. Create and activate a virtual environment

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

macOS or Linux:

```bash
source .venv/bin/activate
```

### 3. Install the required packages

```bash
pip install pandas jupyter
```

### 4. Start Jupyter Notebook

```bash
jupyter notebook Chicago_Payroll_Analysis.ipynb
```

Run the cells in order. Keep the CSV file in the repository root so the notebook can load it through its relative path.

## Compatibility Notes

For explicit currency conversion in current pandas versions, the cleaning steps can be written as:

```python
pay["Salary"] = (
    pay["Annual Salary"]
    .str.replace("$", "", regex=False)
    .astype(float)
)

pay["H_Rate"] = (
    pay["Hourly Rate"]
    .str.replace("$", "", regex=False)
    .astype(float)
)
```

For department-level salary averages, this form avoids version-dependent handling of non-numeric columns:

```python
pay.groupby("Department")["Salary"].mean()
```

## Limitations

- The dataset is a point-in-time snapshot rather than a time series.
- Salary and hourly-rate records are not directly comparable without a clearly defined annualisation method.
- The analysis is descriptive and does not establish causal relationships.
- Employee names can repeat, so the row count should not automatically be interpreted as the number of distinct individuals.
- Extreme or unusual values require validation against the official source.
- The repository currently contains no automated tests, dashboard, or visualisation assets.

## Future Improvements

- add visualisations for department size, salary distribution, and hourly-rate distribution;
- create a reproducible data-cleaning module outside the notebook;
- add a `requirements.txt` file with pinned dependencies;
- validate potential outliers and document data-quality rules;
- build an interactive Streamlit or Power BI dashboard;
- add automated tests for currency conversion and aggregation logic;
- compare multiple payroll snapshots to analyse workforce and compensation trends.

## Responsible Use

Although the dataset is publicly available, it contains employee-level information. Use it responsibly, retain source attribution, avoid unnecessary redistribution of personal data, and do not interpret compensation values without appropriate context.

## Author

**Md. Alif Hossen**

[GitHub](https://github.com/Alif1642) · [LinkedIn](https://www.linkedin.com/in/md-alif-hossen1642) · [Portfolio](https://alif1642.github.io/portfolio/)

## Acknowledgements

Data is provided by the [City of Chicago Data Portal](https://data.cityofchicago.org/Administration-Finance/Current-Employee-Names-Salaries-and-Position-Title/xzkq-xp2w). This repository is an independent educational data-analysis project and is not affiliated with or endorsed by the City of Chicago.
