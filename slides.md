---
title: Leveling-up your Survey Data - A hands-on approach to visualizing survey data with Tableau
separator: <!--s-->
verticalSeparator: <!--v-->
theme: sky
revealOptions:
    transition: 'slide'
---

## Leveling-up your Survey Data - A hands-on approach to visualizing survey data with Tableau

### Mark Green
#### Holy Family University
#### Director of Institutional Research

<!--s-->

## Introduction

* Data is everywhere! 

![Alt Text](https://media.giphy.com/media/VeNDat4n4Kre76oS1g/giphy.gif)
* Let's get lazy! 

![Alt Text](https://media.giphy.com/media/UwjE7m3HGBnby/giphy.gif)

<!--s-->

## Learning Outcomes

* Understand the process of building a visualizaiton in Tableau
* Apply the foundations to apply this on your own

<!--s-->

## Time to Get Started

* Download Tableau (https://www.tableau.com/products/desktop/download)
* Download Datafile (https://github.com/mgreen216/levelupsurveydata/blob/master/Fake%20Survey%20Data%20-%20Leveling-Up.csv)

<!--s-->

## Data Structures

### Wide vs. Tall Data Files
* Each row is a respondent
* Each row is a question response

<!--v-->

# Wide Data


<!--v-->

# Tall Data

<!--s-->

## Preparing your Data

* Data Source
* Data Cleaning
* Data Visualization

<!--s-->

## Next Steps

* Open Tableau
* Connect the Data Source
* Explore the data

<!--s-->

## Tableau Terminology

* Measures
* Dimensions
* Columns 
* Rows 

<!--v-->

### Tableau Terminology (Cont'd)

* Colors
* Size 
* Tooltip
* Label
* Detail
* Shape

<!--s-->

## Build a Bar Chart

* Question to Columns
* SUM(Response Value) to Rows
* Question to Color
* Move SUM(Response Value) to Label
* Move AVG(Response Value) to Label -> Change format to percent
* Filter Question

```
Select Grad School Full-Time, Grad School Part-Time,
Work Full-Time, Work Part-Time
```
<!--s-->

## Build a Dashboard

* Create a chart for race
* Create a chart for gender
* Create a chart for major
* Create a dashboard and bring in the charts
* Add a filter

<!--s-->

## Questions by Program

* Filter Questions
* Move Majors to Rows
* Move Question to Columns
* Move AVG(Response Value) to Columns
* Move CNTD(Student Id) to size

<!--v-->

### Questions by Program (Cont'd)

* Move AVG(Response Value) to Label
* Add Analytics Average Line
* Fixed Question Average
```
{FIXED [Question] : AVG([Response Value])}
```
<!--v-->

### Z-Score
```
(AVG([Response Value]) - SUM([Fixed Question Average]))
/
WINDOW_STDEV(avg([Response Value]))
```

<!--v-->

### Stat Diff
```
IF [Z-Score] >= 2.33 THEN 'Statistically greater p-value < .01'
ELSEIF [Z-Score] >= 1.645 THEN 'Statistically greater p-value < .05' 
ELSEIF [Z-Score] <= -2.33 THEN 'Statistically less p-value < .01'
ELSEIF [Z-Score] <= -1.645 THEN 'Statistically less p-value < .05' 
ELSE 'No statistical difference'
END
```

Change Stat Diff to be calculated Across Major

<!--s-->

## Stacked Likert Scale Data

* Question to Rows
* Filter Questions

<!--v-->

### Total Negative
```
TOTAL(SUM(IF [Response Value] = 1 THEN 1 
ELSEIF [Response Value] = 2 THEN 1
ELSEIF [Response Value] = 3 THEN 0.5
ELSE 0
END))
```
<!--v-->

### Respondents

```
TOTAL(COUNTD([Student Id]))
```

### Start

```
-[Total Negative]/[Respondents]
```

<!--v-->

### Percent of Total

```	
COUNTD([Student Id])/[Respondents]
```
### Gantt Position

```
PREVIOUS_VALUE([Start]) + ZN(LOOKUP([Percent of Total],-1))
```

<!--v-->

* Move Gantt Position to Columns
* Move AVG(Response Value) to Columns
* Move Start to Rows (Change to discreet; Change to compute using Question)
* Move Question to Rows 
* Move Respondents to Rows

<!--v-->

* Question Response to Color
* Percent of Total to Size (Compute Using Question Response)
* Percent of Total to Label (Compute Using Question Reponse)
* Gantt Position Compute Using Question Response

<!--v-->

* Add AVG(Response Value)  to Columns
* Create Dual Axis
* Format Text for Response Value

<!--s-->

# Questions? 

<!--s-->

## Thank you! 

* Mark Green
* email: mgreen2@holyfamily.edu 
