# Mexican Restaurant Ratings Analysis

### Table of Contents
- [Overview](#overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Data Cleaning](#data-cleaning)
- [Problem Statement](#problem-statement)
- [Data Modelling](#data-modelling)
- [Findings/Recommendation](#findings-recommendation)


# Overview
This ia a data analysis project on restaurants based in mexico. A customer survey was carried out in this city in 2012 to collate information about each restaurant, their cuisines, information about their consumers and the preferences of the consumers.There are other additional information you will find in this dataset when exploring it.

## Data Source
"Restaurant rating.csv file format [download here](https://drive.google.com/file/d/1c1HKM8UTqwWOgexRLOtEJuxjBiA2N6xf/view?usp=drive_link)

## Tools
-  Power Query for Data Cleaning
-  SQL Server for Exploratory Data Analysis and Data Modelling
-  Power BI for Data Visualization and Reports

 ## Data Cleaning
 The following tasks were performed for data cleaning and preparation;
 - Data Loading and inspection
 - Handling missing values
 - Data Formating

## Problem Statement
- What can you learn from the highest rated restaurants? Do consumer preferences have an effect on
ratings?

- What are the consumer demographics? Does this indicate a bias in the data sample?

- Are there any demand & supply gaps that you can exploit in the market?
  
- If you were to invest in a restaurant, which characteristics would you be looking for?


![restaurant rating dashboard ](https://github.com/BukolaOrire/Restaurant_Ratings/assets/161165047/f649c57a-9035-49b1-9555-2022473687e3)



## Data Modelling
```sql
SELECT * FROM Consumer_preferences

SELECT * FROM Consumers

SELECT * FROM Restaurants

SELECT * FROM Restaurant_cuisines

SELECT * FROM Ratings

---whats the highest Rated Restaurants?
CREATE VIEW Highest_rating AS 
SELECT A.Restaurant_ID,Name
       ,ROUND(AVG(Overall_Rating),2) AS Avg_overall_rating
       ,ROUND(AVG(Food_Rating),2) AS Avg_food_rating
       ,ROUND(AVG(service_Rating),2) AS Avg_service_rating
FROM Ratings A
INNER JOIN
Restaurants B
ON  A.Restaurant_id = B.Restaurant_id
GROUP BY  A.Restaurant_id,Name

SELECT * FROM Highest_rating
ORDER BY Avg_overall_rating DESC
        ,Avg_food_rating DESC

---Whats are the features of the top highest rating Restautants?
SELECT A.Restaurant_ID,A.Name,Cuisine,Avg_overall_rating
      ,Avg_food_rating,Avg_service_rating,City,State
	  ,Alcohol_Service,Smoking_Allowed,Price,Area,Parking
FROM Highest_rating A
INNER JOIN 
Restaurants B
  ON A.Restaurant_ID = B.Restaurant_ID
INNER JOIN
Restaurant_cuisines C
  ON A.Restaurant_ID = C.Restaurant_ID
ORDER BY Avg_overall_rating DESC,Avg_food_rating DESC

---What are Consumers Demographics of Consumers who rated?
SELECT * FROM Highest_rating A
INNER JOIN
Ratings B ON A.Restaurant_ID=B.Restaurant_ID
INNER JOIN 
Consumers C ON C.Consumer_ID=B.Consumer_ID 
ORDER BY Avg_overall_rating DESC
        ,Avg_food_rating DESC 
		,Avg_service_rating DESC

--- Consumer preferred_Cuisine vs Restaurant_Cuisine and its effect on the Highest Rated Restaurants.
SELECT TOP 26 B.Restaurant_ID,A.Consumer_ID,Name
              ,Cuisine AS Restaurant_Cuisine,Preferred_Cuisine
FROM Ratings A
INNER JOIN 
Highest_rating B 
   ON A.Restaurant_ID=B.Restaurant_ID
INNER JOIN 
Restaurant_cuisines C 
   ON B.Restaurant_ID=C.Restaurant_ID
INNER JOIN 
Consumer_preferences D 
    ON A.Consumer_ID=D.Consumer_ID
ORDER BY Avg_overall_rating DESC
        ,Avg_food_rating DESC 
		,Avg_service_rating DESC

---Conducting Analysis on Consumer Demographics by Age_group
SELECT Age_group,Drink_Level
      ,COUNT(Drink_level) AS Alcohol_consumer_count
FROM
(SELECT Drink_level,
CASE WHEN Age BETWEEN 18 AND 30 THEN 'Young Adult'
     WHEN Age BETWEEN 31 AND 50 THEN 'Adult'
	 ELSE 'Old Adult' END AS Age_group
	 FROM Consumers)
Consumers
GROUP BY Age_group,Drink_Level
ORDER BY 1
-------
SELECT Age_group,Smoker
	 ,COUNT(Smoker) AS Smoker_count
FROM
(SELECT Smoker,
CASE WHEN Age BETWEEN 18 AND 30 THEN 'Young Adult'
     WHEN Age BETWEEN 31 AND 50 THEN 'Adult'
	 ELSE 'Old Adult' END AS Age_group
	 FROM Consumers)
Consumers
GROUP BY Age_group,Smoker 
ORDER BY 1
------
SELECT Age_group,Transportation_Method
	 ,COUNT(Transportation_Method) AS Transport_count
FROM
(SELECT Transportation_Method,
CASE WHEN Age BETWEEN 18 AND 30 THEN 'Young Adult'
     WHEN Age BETWEEN 31 AND 50 THEN 'Adult'
	 ELSE 'Old Adult' END AS Age_group
	 FROM Consumers)
Consumers
GROUP BY Age_group,Transportation_Method
ORDER BY 1
------
SELECT Age_group,Budget
	 ,COUNT(Budget) AS Budget_count
FROM
(SELECT Budget,
CASE WHEN Age BETWEEN 18 AND 30 THEN 'Young Adult'
     WHEN Age BETWEEN 31 AND 50 THEN 'Adult'
	 ELSE 'Old Adult' END AS Age_group
	 FROM Consumers)
Consumers
GROUP BY Age_group,Budget
ORDER BY 1

----Whats the Highest Preferred Cuisine by Consumers? and What Cuisine is offered the most in Rated Restaurants?
WITH Consumers AS (
SELECT preferred_cuisine
      ,COUNT(Preferred_cuisine) AS Consumer_Count
FROM Consumer_preferences
GROUP BY Preferred_Cuisine),
Restaurants AS (
SELECT cuisine AS Restaurant_Cuisine
       ,COUNT(cuisine) AS Restaurant_Count
FROM Restaurant_cuisines
GROUP BY cuisine)
SELECT * 
FROM Consumers 
FULL OUTER JOIN Restaurants
ON Preferred_Cuisine=Restaurant_Cuisine
ORDER BY Consumer_Count DESC,Restaurant_Count DESC 
 
---- Conducting Analysis on Restaurants Demograhics and compare with Consumer Demographics
SELECT Parking,COUNT(Parking) AS Parking_Count
FROM Restaurants
GROUP BY ROLLUP (Parking)

CREATE VIEW R_Demo AS 
SELECT Name,Consumer_ID,Price,state,parking
      ,Smoking_Allowed,Alcohol_Service
FROM Restaurants A
INNER JOIN Ratings B
ON A.Restaurant_ID = B.Restaurant_ID

----Is there an Equilibrum in demand(Consumers) Vs supply(Restaurants)and is it stable or unstable?
----Restaurants With the Highest  Average Ratings and Compare with Consumers Demographics and Restaurants Demographics
SELECT R.Name,R.state,R.Consumer_ID,Price,Budget,parking
      ,Smoking_Allowed,Smoker,Alcohol_Service, Drink_Level
	  ,Children,Occupation
FROM R_Demo R
INNER JOIN Consumers C
ON R.Consumer_ID = C.Consumer_ID
INNER JOIN Highest_rating D
ON R.Name = D.Name 
WHERE Avg_overall_rating = '2'
ORDER BY Avg_overall_rating DESC,Avg_food_rating DESC
----Restaurants with the least Average Ratings and Compare with Consumers Demographics and Restaurants Demographics
SELECT TOP 14  R.Name,R.state,R.Consumer_ID,Price,Budget,parking
      ,Smoking_Allowed,Smoker,Alcohol_Service, Drink_Level
	  ,Children,Occupation
FROM R_Demo R
INNER JOIN Consumers C
ON R.Consumer_ID = C.Consumer_ID
INNER JOIN Highest_rating D
ON R.Name = D.Name 
WHERE Avg_overall_rating IN ('0.25','0.50')
ORDER BY Avg_overall_rating ASC
        ,Avg_food_rating ASC
        ,Avg_service_rating ASC
```

## Findings and Recomendation	




