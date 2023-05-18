# Road_Accident_Analysis

![image](https://github.com/abhishekpattajoshi/Road_Accident_Analysis/assets/131600014/a5f31593-fae0-455f-bffe-eea46f04ccd1)

## Objective
Clients wants to create a Road Accident Dashboard for year 2021 and 2022 so that they can have insight on the below requirements-
- Primary KPI-Total Casualties and Total Accident values for Current Year and YoY growth
- Primary KPI's-Total Casualties by Accident Severity for Current Year and YoY growth
- Secondary KPI's-Total Casualties with respect to vehicle type for Current Year
- Monthly trend showing comparison of casualties for Current Year and Previous Year
- Casualties by Road Type for Current year
- Current year casualties by Area/Location and by Day & Night
- Total casualties and Toatal accidents by location

## Data Processing
- We created calendar table where we extracted dates, year, month and then merged the table with main table
- We used CALENDAR() which return a table with one column of all dates between start date and end date
  * Calendar=CALENDAR(Min(Data[AccidentDate]),Max(Data[AccidentDate]))
- We added another column name Year which is extracted from Accident Date by using Year()
  * Year=YEAR(Calendar[Date])
- We added another column name Month which is extracted from Accident Date by using Format()
  * Month=Format(Calendar[Date,"mmm"])
- We calculated current year casualties by using TOTALYTD() which evaluates the specified expression over the interval which begins on the first day of the year and ends with the last date in specified date column after applying specified filters
  * CY Casualties=TOTALYTD(Sum(Data[Number_of_casualties]),Calendar[Date])
- To calculate YOY growth we need to calculate previous year casualties by using SAMEPERIODLASTYEAR() which returns a set of data in the current selection from previous year
  * PY Casualties=Calculate(Sum(Data[Number_of_Casualties]),SAMEPERIODLASTYEAR(Calendar[Date]))
  * YoY Casualties=([CY Casualties]-[PY Casualties])/[PY Casualties]  
