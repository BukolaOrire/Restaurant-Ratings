# Mexico Restaurants Rating Analysis


### Table of Contents
- [Overview](#overview)
- [Data Source](#data-source)
- [Skills](#skills)
- [Data Cleaning](#data-cleaning)
- [Problem Statement](#problem-statement)
- [Data Modelling](#data-modelling)
- [Conclusion](#conclusion)


# Overview
This is a data analytics project on restaurants based in mexico. A customer survey was carried out in 2012 to collate information about each restaurant, their cuisines, information about their consumers and the preferences of the consumers.The purpose and objective of this project is to improve consumer satisfaction and patronage thereby maximizing sales, profit and providing adequate information to potential investors and business entrepreneurs who are looking to invest in the restaurant business.
**_Disclaimer_**: _All datasets and reports do not represent any company, institution or country, but just a dummy dataset to demonstrate capabilities of power BI._**

## Data Source
"Restaurant rating.csv file format [download here](https://drive.google.com/file/d/1c1HKM8UTqwWOgexRLOtEJuxjBiA2N6xf/view?usp=drive_link) This Dataset was provided by Digitaleydrive as part of my capstone project.
This Dataset consists of  5 tables 

## Skills
-  Power Query for Data Cleaning
-  Power BI for Data Modelling and Report

 ## Data Cleaning
 The following tasks were performed for data cleaning and preparation;
 - Data Loading and Transformation
 - Handling missing values
 - Data Validation 

## Problem Statement
1. What can you learn from the highest rated restaurants? Do consumer preferences have an effect on ratings?
2. What are the consumer demographics? Does this indicate a bias in the data sample?
3. Are there any demand & supply gaps that you can exploit in the market?
4. If you were to invest in a restaurant, which characteristics would you be looking for?


## Data Modelling
Automatically derived relationships are adjusted to repalce and add relationships with the required.

Adjusted Model     |        Auto Model
:-----------------:| :-------------------:
![Adjusted_model](https://github.com/BukolaOrire/Restaurant_Ratings/assets/161165047/8fced2bc-ca0e-42b9-a67d-621cc94ebe23)  |   ![auto_model](https://github.com/BukolaOrire/Restaurant_Ratings/assets/161165047/9385bad0-a449-4606-b47e-6c7aa6d6504b)


The model is a snowflake schema.
There are 7 dimension tables and 1 fact table.The dimension tables are all joined to the fact table with many-to-one relationship.

## Data Visualization
The Report comprises of 3 pages outlined below:
1.  Restaurant Demograhics
2.  Consumer Demographics
3.  Restaurant Rating Analysis

![consumer_demographics](https://github.com/BukolaOrire/Restaurant_Ratings/assets/161165047/86b30661-b924-423a-90b4-32e116c8a47c)

![restaurant_demograhics](https://github.com/BukolaOrire/Restaurant_Ratings/assets/161165047/508fb9ff-1f3d-4ee4-bac2-24a15af5b01e)

![restaurant_rating_analysis](https://github.com/BukolaOrire/Restaurant_Ratings/assets/161165047/1b91e047-55f0-4f93-93a3-912fcf5b14d3)

![restaurant_rating_analysis2](https://github.com/BukolaOrire/Restaurant_Ratings/assets/161165047/48604dc6-7d7f-4ee5-a4cf-5c62884126ae)



## Conclusion
- The Analysis conducted  indicates  there is a gap between demand and supply by cuisine. At least 50% of Consumers prefer Mexican cuisine compared to other cuisines, but 
  not up to  40% of Restaurants  are offering Mexican cuisine. There are 78 other cuisines consumers prefer but no restaurant is offering these cuisines. Restaurants should 
  make provisions to include food diversity and expand their menu to include additional cuisines that may  help solve the demand and supply gap and improve consumer 
  satisfaction and also  maximize profit. The results also proves that consumers aged 18 to 30 (Young Adults)  have  the highest level of patronage .
  
- Further analysis also revealed  that consumer food preference had no direct impact on the success of the restaurants, as observed among the highest rated restaurants. 
  There are other factors that may influence consumers decision to patronize a restaurant, such as the overall service and convenience of the restaurant and its 
  environment, staff conduct, location, restaurant interior and ambience etc.
  
- The top 3 highest rated restaurants; Restaurant las mananitas, Emilianos, and michiko restaurant jopanes offers at least 70% of the services consumers are interested in, 
   and there are little to no constraints in restaurant  demographics when compared to consumer demographics. There is still need for improvement on services rendered by 
   these restaurants.
  
- Potential investors looking to invest in the  restaurant business must conducted proper research and analysis on major factors such as location of the restaurant, 
  competition, rate of return, return on Investment, capability, type of Menu etc. In this Scenario, San Luis Potosi is the top best restaurant location for possible 
  investment.






















