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

  | Age_Group | Satisfied |
  | --------- | --------- |
   | 18-25    | 6358      |
   | 26-35    |  8873     |
   | 36-45    |  15942     |
   | 46-56    |    16485    |
   | 57+      |  8770      |
   

 The SQL query categorizes airline passengers into different age groups and counts the number of satisfied passengers in each group. The results show that the 46-56 age group has the highest number of satisfied passengers (16,485), followed closely by the 36-45 age group (15,942). The 26-35 and 57+ age groups have 8,873 and 8,770 satisfied passengers, respectively, while the 18-25 age group has the lowest count at 6,358. The data is ordered by age group for better readability.



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

| Food_and_Drink | Total_Passengers|Satisfaction_Rate|
| -------------- | ---------------- |-----------------|
|         5	     |        27957      |    55.088171119934|
|         4	     |         30563	    |    52.583188823086 |
 |         0	    |      132	         |     41.666666666666|
  |        3	      |      27794	        |    39.742390443980|
   |       2	    |      27383	         |       38.900047474710|
   |       1	    |       16051	        |      19.955142981745|


  The SQL query analyzes passenger satisfaction based on ratings for Food and Drink services. It groups passengers by their Food_and_Drink rating (from 0 to 5) and calculates the total number of passengers in each category along with the satisfaction rate (percentage of satisfied passengers).

The results indicate that passengers who rated Food and Drink as 5 had the highest satisfaction rate (55.09%), followed by those who rated it 4 (52.58%). Conversely, passengers who gave the lowest rating (1) had the lowest satisfaction rate (19.96%), suggesting a strong correlation between food quality and overall satisfaction.



 - Determining  the average delay (departure + arrival) for each airline class,but only for flights where passengers were dissatisfied.



```SQL
  SELECT
          class,
ROUND
(AVG("Departure_Delay"+"Arrival_Delay"),2) As Flight_Delay
FROM
airline_passenger_satisfaction
WHERE
 Satisfaction = 'Neutral or Dissatisfied'
GROUP BY
 class
 ```

|Class|Flight_Delay|
|-----|------------|
|Economy|	32.52|
|Business	|35.36|
|Economy Plus|	33.98|

The SQL query calculates the average total flight delay (sum of departure delay and arrival delay) for each airline class, but only for flights where passengers were neutral or dissatisfied with their experience.

The results show that Business class has the highest average flight delay (35.36 minutes), followed by Economy Plus (33.98 minutes) and Economy (32.52 minutes). The analysis helps in identifying the impact of delays on customer satisfaction across different airline classes.



 - Finding the average cleanliness rating for satisfied and dissatisfied passengers.
```SQL
SELECT
       Satisfaction,
AVG(Cleanliness) as Cleanliness_Rating
FROM
       airline_passenger_satisfaction
GROUP BY
      Satisfaction
ORDER BY
           Cleanliness_Rating DESC
```

|Satisfaction|Cleanliness_Rating|
|------------|------------------|
|Satisfied   |	3  |
|Neutral or Dissatisfied	|2      |


This  query calculates the average cleanliness rating for passengers based on their satisfaction level. It groups passengers into two categories: Satisfied and Neutral or Dissatisfied, then computes the average cleanliness rating for each group.

The results show that satisfied passengers rated cleanliness higher, with an average score of 3, while neutral or dissatisfied passengers gave a lower rating of 2. This suggests that cleanliness plays a significant role in passenger satisfaction and may be a key factor in improving overall airline service quality.
```SQL
SELECT  
          Class, 
       COUNT(In_flight_Entertainment) AS total_passengers,
       COUNT(CASE WHEN "In_flight_Entertainment" <= 3 THEN 1 END) AS Low_star_ratings
FROM 
airline_passenger_satisfaction
GROUP BY 
          Class
ORDER BY 
       Low_star_ratings DESC
```
|Class|Total_Passengers|Low_star_ratings|
|-----|----------------|----------------|
|Economy|	58309|	33491|
|Business	|62160	|22721|
|Economy Plus|	9411|	5333|

This  query evaluates the number of passengers in each airline class and identifies how many of them gave low ratings (3 or below) for in-flight entertainment. Economy Class Receives the Most Low Ratings 33,491 passengers in Economy gave a low rating, the highest among all classes.This suggests that in-flight entertainment in Economy may need significant improvements.Business Class Has the Second-Highest Low Rating 22,721 passengers in Business Class rated in-flight entertainment 3 or lower.Economy Plus Shows the Lowest Complaint Rate:Only 5,333 passengers in Economy Plus reported dissatisfaction.

This suggests that in-flight entertainment might be slightly better in Economy Plus class compared to others.


 - List of passenger dissatisfied with wifi service
```SQL
select 
      In_flight_service,
Count(*) As Diss_service
From 
      airline_passenger_satisfaction
where 
     Satisfaction = 'Neutral or Dissatisfied'
Group by 
        In_flight_service
Order by  
        Diss_service
```
|In_flight_service|Diss_service|
|-----------------|------------|
|0                 |	5|
 |1	     |6274|
|2	|10003|
|5	|13246|
|3|	19233|
|4|	24691|

Majority of Dissatisfied Passengers Rated Service Between 3 and 5. 24,691 passengers rated in-flight service 4, the most common rating among dissatisfied passengers.19,233 passengers gave a rating of 3, indicating a large number of passengers found the service average but not satisfactory.13,246 passengers rated it 5, suggesting that even some passengers who gave a high rating to in-flight service were still dissatisfied overall.

 - Recommendations:
   
Investigate why many dissatisfied passengers still rated in-flight service 4 or 5.

Improve service quality for passengers rating in-flight service 3 and below by addressing common complaints.

Also, improving in-flight service, airlines can reduce dissatisfaction and enhance overall passenger experience.



### Recommendation Report: Airline Passenger Satisfaction Analysis
 - Key Findings:
 - Delays Impact All Classes:

 - Business class has the highest average flight delay (35.42 minutes), followed by Economy Plus (34.08 minutes) and Economy (32.59 minutes).

Delays may significantly contribute to dissatisfaction among passengers.

 - Cleanliness Matters

Satisfied passengers rated cleanliness at 3.75, while dissatisfied passengers gave it a lower score of 2.93.

This indicates that maintaining a clean environment is essential for improving customer satisfaction.

 - Check-in Service Complaints are High

43,783 dissatisfied passengers reported issues with check-in services (rating 3 or below).

Streamlining check-in processes can improve the passenger experience.

 - Upgrade in-flight entertainment in Economy and Business classes by adding more content variety, improving screen quality, and ensuring better functionality.

 - Improve WiFi connectivity to enhance streaming experiences.


### Actionable Recommendations
 - Reduce Flight Delays:

 - Identify operational inefficiencies causing delays, especially in Business Class.

 - Improve scheduling and turnaround times to reduce wait times.

 - Improve Cleanliness environment.

  - Enhance Check-in Services on time 


Upgrade In-flight Entertainment & WiFi:

Expand entertainment selections and improve screen quality.

Enhance WiFi connectivity to provide a smoother browsing experience.


### Conclusion:
The analysis highlights critical service gaps affecting passenger satisfaction, particularly in delays, cleanliness, check-in service,food and drinks, and in-flight WiFi. Addressing these concerns can significantly improve customer experience and loyalty.

Thank you for reading. ​




