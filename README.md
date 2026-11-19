# Power BI PR4 — HR Analytics with DAX

## Project Overview
This project builds a DAX-focused HR analytics dashboard in Power BI using the
Employee / HR Dataset All in One from Kaggle.

## Dataset
-**Name:** Employee / HR Dataset All in One
-**Author:** Ravindra Singh Rana
-**Files:** 5 CSV files
-**Rows:** 50,000+ across all files

## Data Model
-EmployeeMaster (Fact)
-Training (Fact)
-EngagementSurvey (Fact)
-Performance (Fact)
-Recruitment (Standalone)
-DimDate (Calendar)

## Relationships (4 Active + 1 Inactive)
| From | To | Column | Cardinality | Filter |
| :--- | :--- | :--- | :--- | :--- |
| EmployeeMaster | Training | Employee ID | 1:* | Single |
| EmployeeMaster | EngagementSurvey | Employee ID | 1:* | Single |
| EmployeeMaster | Performance | Employee ID | 1:* | Single |
| DimDate | EmployeeMaster | DateOfJoining | 1:* | Single |
| DimDate | EmployeeMaster | DateOfTermination | 1:* | Inactive |

## Calculated Columns (10)
| Name | Table | Business Use |
| :--- | :--- | :--- |
| Tenure_Years | EmployeeMaster | Years of service |
| Career_Level_Band | EmployeeMaster | Career classification |
| Full_Name | EmployeeMaster | Display name |
| Salary_Band | EmployeeMaster | Compensation band |
| Is_Active | EmployeeMaster | Active flag |
| Performance_Label | EmployeeMaster | Rating description |
| Salary_Formatted | EmployeeMaster | Formatted salary |
| Days_Since_Hire | EmployeeMaster | Days since joining |
| Hire_Year_Month | EmployeeMaster | YYYY-MM period |
| Above_Avg_Salary_Flag | EmployeeMaster | Above average flag |

## Measures (25+)
| Name | Formula | Business Use |
| :--- | :--- | :--- |
| Total_Headcount | COUNTROWS(EmployeeMaster) | Baseline KPI |
| Active_Headcount | CALCULATE(COUNTROWS, status="Active") | Active employees |
| Terminated_Count | CALCULATE(COUNTROWS, status="Terminated") | Terminated employees |
| Avg_Salary | AVERAGE(Salary) | Average salary |
| Total_Salary_Cost | SUM(Salary) | Total payroll |
| Avg_Tenure | AVERAGE(Tenure_Years) | Average tenure |
| Distinct_Departments | DISTINCTCOUNT(DepartmentType) | Unique departments |
| Avg_Performance_Rating | AVERAGE(Current Employee Rating) | Average rating |
| Attrition_Rate_% | DIVIDE(Terminated, Total) | Key HR KPI |
| Gender_Diversity_Ratio | DIVIDE(Female Active, Active) | Diversity metric |
| Bench_Utilisation_% | DIVIDE(Underperforming, Active) | Bench metric |
| Avg_Training_Cost | AVERAGEX(Training, Cost) | Average training cost |
| Total_Training_Cost | SUMX(Training, Cost) | Total training investment |
| Total_HC_All_Depts | CALCULATE(Total, ALL) | Cross-department total |
| Headcount_%_of_Total | DIVIDE(Total, All Depts) | % of total |
| Dept_Avg_Salary_AEXCEPT | CALCULATE(Avg_Salary, ALLEXCEPT) | Department benchmark |
| High_Performers_Count | CALCULATE(Active, rating>=4) | High performers |
| High_Performer_% | DIVIDE(High, Active) | % high performers |
| Senior_Headcount | CALCULATE(Active, FILTER(tenure>=8)) | Senior employees |
| Salary_Rank_Dept | RANKX(depts, Avg_Salary) | Salary ranking |
| Training_Cost_Rank | RANKX(depts, Training Cost) | Training ranking |
| YTD_New_Hires | TOTALYTD(Total, Date) | YTD hiring |
| New_Hires_SPLY | SAMEPERIODLASTYEAR | Prior year hires |
| New_Hires_YoY_% | YoY growth in hiring | Hiring growth |
| Hires_Prior_3M | DATEADD(-3, MONTH) | Lag analysis |
| Attrition_Rate_YTD | TOTALYTD + USERELATIONSHIP | YTD attrition |

## Tools Used
-Power BI Desktop
-Power Query (for DimDate creation)
-DAX (for calculated columns and measures)

## Screenshots
(Add screenshots of Model View, `_Measures` table, and all 3 report pages)

## Video Link
(Add your video link here)
