# Diversity-and-inclusion

![1536548107152](https://github.com/user-attachments/assets/ed030d66-a9be-4907-b16f-705db48f4e75)

## Table of Content
- [Problem Statement](#problem-statement)
- [Data Source](#data-source)
- [Tools](#tools)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Data Analysis](#data-analysis)
- [Data Visualization](#data-visualization)
- [Insights](#insights)
- [Recommendations](#recommendations)
  
## Problem Statement
The purpose of this task is to:

* Define proper KPIs in hiring, promotion, performance and turnover
* Create a visualisation for the HR manager that reflects all relevant Key Performance indicators(KPIs) and metrics in the dataset.

## Data Source
Dataset used for this task was presented by [Pwc](https://www.pwc.ch/en/careers-with-pwc/students/virtual-case-experience.html) and Diversity and Inclusion dataset:

Dataset: [Diversity and Inclusion](https://github.com/yogeshkasar778/PWC_task3-Diversity_and_Inclusion_dashboard/blob/main/03%20Diversity-Inclusion-Dataset.xlsx)

## Tools
PowerBi, Power Query

## Data Cleaning and Preparation

Completed the Data transformation in Power Query and the dataset loaded into Microsoft Power BI Desktop for modeling.

- `Diversity and Inclusion dataset` which has `500 rows and 31 Column` of observation

Data Cleaning for the dataset was done in the power query editor as follows:
- Changed the header row of dataset
- Replaced  the value is `New hire FY20?` N coverted No and Y converted Yes
- Replaced  the value is `In base group for turnover FY20` N coverted No and Y converted Yes
- Replaced  the value is `Promotion in FY20?` N coverted No and Y converted Yes
- Removed Unnecessary columns 
- Removed Unnecessary rows
- Each of the columns in the table were validated to have the correct data type

![D   i 3](https://github.com/user-attachments/assets/71a11843-14f4-448e-be3c-7255129bcce5)

## Data Analysis
measures defined for analysis are:

``` DAX
# of emp FY21 = CALCULATE(
    DISTINCTCOUNT('Pharma Group AG'[Employee ID]),
    FILTER('Pharma Group AG','Pharma Group AG'[FY20 leaver?] <> "Yes"))

# of female new hire = CALCULATE(
    '_measures'[# of new hire FY20], 'Pharma Group AG'[Gender] = "Female")

# of FY21 promotee = CALCULATE(
    '_measures'[# of emp FY21],'Pharma Group AG'[Promotion in FY21?] = "Yes")

# of male new hire = CALCULATE(
    '_measures'[# of new hire FY20], 'Pharma Group AG'[Gender] = "Male")

# of FY20 leavers = CALCULATE(
    DISTINCTCOUNT('Pharma Group AG'[Employee ID]),'Pharma Group AG'[FY20 leaver?] = "Yes")

# of FY20 promotee = CALCULATE(
    DISTINCTCOUNT('Pharma Group AG'[Employee ID]),'Pharma Group AG'[Promotion in FY20?] = "Y")

# of new hire FY20 = CALCULATE('_measures'[# of emp FY21],'Pharma Group AG'[New hire FY20?] = "Y")

% of Turnover = 
VAR in_base_grp_of_turnover =
    CALCULATE(
        DISTINCTCOUNT( 'Pharma Group AG'[Employee ID] ),
        'Pharma Group AG'[In base group for turnover FY20] = "Y"
    )
VAR leavers = '_measures'[# of FY20 leavers]
VAR TotalEmployees =
    CALCULATE(
        DISTINCTCOUNT( 'Pharma Group AG'[Employee ID] )
    )
VAR avg_emp = DIVIDE((in_base_grp_of_turnover + leavers) + TotalEmployees,2)
VAR TurnoverRate =
    DIVIDE( leavers, avg_emp ) * 100
RETURN
    TurnoverRate

female FY20 avg rating = CALCULATE(
    '_measures'[FY20 avg rating],'Pharma Group AG'[Gender] = "Female")

FY20 avg rating = AVERAGE('Pharma Group AG'[FY20 Performance Rating])

male FY20 avg rating = CALCULATE(
    '_measures'[FY20 avg rating],'Pharma Group AG'[Gender] = "Male")
```

## Data Visualization

Data visualization for the data analysis (DAX) was done in Microsoft Power BI Desktop:

[Dashboard Report](https://app.powerbi.com/view?r=eyJrIjoiNDYyY2ZiNzEtZGE3OC00YWY4LWIwMGItMzIyOTkxOGU1NWQwIiwidCI6IjI2MTRhZTljLTQ2MmUtNDMyMi05MGE4LWRkMmNkYzYyM2ZjNiJ9)

![D   i 1](https://github.com/user-attachments/assets/4fe0ceba-d0eb-4f6c-a1ee-19edcf8acb62)

![D   i 2](https://github.com/user-attachments/assets/8a6af5ef-9f66-497d-ae4a-2779652c5909)


## Insights

As shown the data Visualization, It can be deduced that:

- 34 Female hires of the year and 32 Male hires of the years.
- total number of employees in 2021 is 453 (269 male, 184 female)
- 18 promoted Female for the year.
- 33 promoted Male for the year.
- Director is the highest Average time of job level promoted in this year.
- Finance department (11.11%) highest turnover of the year.
- Average Rating Female 2.42%
- Average Rating Male 2.41%
- Employees promoted in year of 2020 is 28 Male and 8 Female.
- The most common age group is 20-29 having 223 employees fall in Junior Officer category.

## Recommendations
- Conduct a gender parity audit to identify potential biases in the promotion process.
- Implement mentorship programs targeted at female employees to help them advance in their careers.
- Create a supportive work environment with regular check-ins and employee feedback mechanisms.
- Conduct exit interviews to understand why employees are leaving the Finance department.
- Conduct employee satisfaction surveys to identify key areas of concern, and address systemic issues such as workload, communication, and resource allocation that may impact employee satisfaction.
