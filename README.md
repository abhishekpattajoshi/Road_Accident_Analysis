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
- Total casualties and Total accidents by location

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
- Similarly for accident severity KPI we have to calculate previous year accidents and year on year accidents using formula
  * PY Accidents=Calculate(COUNT(Data[Accident Index],SAMPLEPERIODLASTYEAR(CALENDAR[Date]))
  * YoY Accidents=([CY Accidents]-[PY Accidents])/[PY Accidents]
- For making secondary KPI of number of vehicles we have merged-
  * Motorcycle of 125cc, 50cc, 125-500cc, over 500cc, pedal cycle into one group named Bike
  * Bus,coach with 17 or more seat, minibus into one category named Bus
  * Car and taxi into one category named Car
  * Other vehicles and horse ridder into other
  * Goods of 3.5-7.5tonnes,goods of 7.5tonnes and below 3.5tonnes as Van
- We used weather conditions as slicer we merged Fine with highwinds, Fine with no high winds as Fine
  * Raining with highwinds,rain with no highwinds as Rain
  * Snowing with highwinds,snow with no highwinds, fog and mist as snow
- We used road conditions as another slicer, we merged flood or wet road into Wet, Frost and Snow as Ice and Dry category

## Visualisation Insights
- CY Casualties is 195.7k and there is reduction of 11.89% from previous year
- CY Accidents is 144.4k and there is reduction of 11.7% from previous year
- CY Fatal accidents is 1.5k and there is reduction of 35.57% from previous year
- CY Serious accidents is 18.8k and there is reduction of 14.51% from previous year
- CY Slight accidents is 124.1k and there is reduction of 10.84% from previous year
- If we look at the kpi casualties by vehicles type we can clearly see the most no of accidents happens in car compare to other vehicles
- If we compare the month to month casualty rate, it has reduced compare to the previous year
- Majority of the accidents have happened in single carriageway comapared to the other roadways
- Majority of accidents happened in day time compared to night time.
- Most of the casualty happened in urban area
- By looking at the map we come to know that casualty rate is higher in cities like london, birmingham and manchester

## Suggestion
- People who are travelling in car should drive carefully because majority of accidents happened with cars
- People should drive carefully on single carriageway and avoid overtaking on single roads, govt should also work in making dual carriageway where accidents rate is lower
- People living in urban area should drive slowly because population is more in this area




