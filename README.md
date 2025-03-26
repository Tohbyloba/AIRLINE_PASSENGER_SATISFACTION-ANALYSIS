# AIRLINE_PASSENGER_SATISFACTION-ANALYSIS
This SQL-based analysis of airline passenger satisfaction reveals significant trends in service quality and operational performance.

## Table of Content
 - Project Overview
 - Project Scope
 - Business Objective
 - Purpose of the Dataset
 - Use Case
 - Data Source
 - Dataset Overview
 - Data Cleaning and Processing
 - Data Analysis and Insight
 - Recommendation
 - Conclusion

## Overview of the dataset
The project focuses on analyzing airline passenger satisfaction based on survey responses and operational data. The dataset includes information on passenger demographics, flight details, and ratings for various aspects of the travel experience. The analysis aims to identify key factors influencing passenger satisfaction, including service quality, comfort, and operational efficiency. Additionally, trends related to flight delays, class preferences, and customer types will be examined to provide actionable insights for improving airline services.

## Project Scope
•	Time Period: Analysis of passenger satisfaction data from recorded survey responses.

•	Geographical Scope: Includes data from various airline routes and classes.

•	Satisfaction Focus: Passenger feedback on different aspects of the flight experience, including service quality, seat comfort, and in-flight entertainment.

•	Key Variables: Passenger demographics, flight details (e.g., class, distance), service ratings, delay times, and overall satisfaction levels.

##	Purpose of the Dataset

This dataset is intended for educational and analytical purposes, enabling researchers, students, and professionals to enhance their data analysis skills. Users can explore key trends in airline passenger satisfaction, identify pain points, and apply data manipulation, visualization, and statistical techniques to extract meaningful insights. By analyzing this dataset, users can better understand the factors influencing customer satisfaction in the airline industry and develop strategies for service improvement and operational efficiency.




## Data Source
The dataset for this project is sourced from Maven Analytics [website](https://app.mavenanalytics.io/datasets?search=Airline+pa) designed for practice purposes. The dataset consists of structured tables containing information on passenger satisfaction ratings, flight details, and customer demographics.The dataset is in a structured format and comprises several key tables:

### • Analysis:

o	Determining which factors contribute most to overall satisfaction.

o	Calculating the percentage of satisfied passengers for each type of travel.

o	Assessing differences in satisfaction between flight classes and customer types.

o	Evaluating the impact of delays on passenger satisfaction.

o	Finding the average flight distance for passengers traveling for business vs. personal travel.

o	Counting the number of passengers who are first-time customers.

o	Retrieving all passengers who are satisfied with their experience.

o	Identifying the  passengers who gave the highest ratings for both "Seat Comfort" and "Leg Room Service.

o	Determine if younger passengers (under 30) are more likely to be satisfied compared to the older passengers.

o	Identify passengers who traveled the longest distance but had the lowest satisfaction rating.

## Objectives
•	Enhance Customer Experience: By analyzing passenger feedback, airlines can identify key areas for service improvements, leading to a more positive travel experience.

•	Increase Customer Retention: Understanding factors that drive passenger satisfaction helps airlines develop strategies to improve loyalty and repeat business.



•	Optimize Operational Performance: Evaluating the impact of delays and service quality on satisfaction allows airlines to refine processes for better efficiency.

•	Identify Areas of Improvement: Analyzing satisfaction trends helps pinpoint specific service aspects, such as seat comfort or in-flight entertainment, that require enhancement.

•	Competitive Benchmarking: The insights from this analysis can serve as a benchmark for tracking improvements over time and staying competitive in the airline industry.


## Data Cleaning and Processing
 
The dataset contains 129,880 entries and 24 columns. It is generally well-structured, with appropriate data types for each column. 
The following procedures were carried out during the data processing phase.

- 1. Created New column
  
A new column was added to enhance the dataset and enable more detailed analysis.

```SQL
ALTER TABLE
airline_passenger_satisfaction
ADD
 Airport_Id INT
UPDATE
 airline_passenger_satisfaction
SET
Airport_Id = ID
```


 - •	Airport_ID: This column represents the Airport_ID for each passengers. Below is the SQL code used to create and update the column;
   
- Do Airline Passenger Satisfaction Levels Fluctuate Based on Travel Patterns?
   
- This analysis aims to determine whether airline passenger satisfaction levels fluctuate based on travel patterns over time. Identifying trends in satisfaction can provide valuable insights into passenger behavior, service quality, and external factors that may influence customer experiences.


Understanding these patterns allows airlines to make data-driven decisions to enhance customer satisfaction. For example, if satisfaction levels decline during high-traffic periods—such as holidays or peak travel seasons—airlines can optimize staffing, improve service offerings, or adjust flight schedules to better accommodate passenger needs.


Additionally, recognizing trends in satisfaction can help airlines refine their marketing and operational strategies, proactively addressing common passenger concerns before they lead to dissatisfaction.
In summary, analyzing variations in passenger satisfaction over time enables airlines to improve service quality, efficiently allocate resources, and enhance the overall travel experience. This insight is particularly valuable for major airlines, as it plays a crucial role in maintaining brand reputation, fostering customer loyalty, and staying competitive in the industry.

```SQL
SELECT
    CASE
        WHEN Age BETWEEN 18 AND 25 THEN '18-25'
        WHEN Age BETWEEN 26 AND 35 THEN '26-35'
        WHEN Age BETWEEN 36 AND 45 THEN '36-45'
        WHEN Age BETWEEN 46 AND 56 THEN '46-56'
        ELSE '57+'
    END AS Age_Group,
    COUNT(*) AS Satisfied_Count
FROM 
airline_passenger_satisfaction
WHERE 
Satisfaction = 'Satisfied'
GROUP BY 
        CASE
        WHEN Age BETWEEN 18 AND 25 THEN '18-25'
        WHEN Age BETWEEN 26 AND 35 THEN '26-35'
        WHEN Age BETWEEN 36 AND 45 THEN '36-45'
        WHEN Age BETWEEN 46 AND 56 THEN '46-56'
        ELSE '57+'
    END 
ORDER BY
 Age_Group;
```

Age_Grop      Satisfied_count
18-25	         6358
26-35	         8873
36-45	          15942
46-56	          16485
57+	          8770

•	Analyze key aspect  if food and drink quality impacts satisfaction.
```SQL
SELECT 
    "Food_and_Drink",
    COUNT(*) AS Total_Passengers,
    COUNT(CASE WHEN Satisfaction = 'Satisfied' THEN 1 END) * 100.0 /COUNT(*) AS Satisfaction_Rate
FROM
 airline_passenger_satisfaction
GROUP BY
 "Food_and_Drink"
ORDER BY 
 Satisfaction_Rate DESC
```

Food_and_Drink      Total_Passengers       Satisfaction_Rate
           5	                         27957	                55.088171119934
          4	                         30563	               52.583188823086
          0	                         132	                41.666666666666
          3	                        27794	                 39.742390443980
          2	                        27383	                  38.900047474710
          1	                        16051	                   19.955142981745


