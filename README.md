# San_Francisco_Crime_Categorization
## Objective
The purpose of this project is to analyse distribution and category of crime in San Francisco Bay area for the past 12 years of data provided by San Francisco Police Department. This work based on the competition named San Francisco Crime Classification conducted by Kaggle.This result will help San Francisco Police Department(SFPD) to eliminate the challange in allocating workforce in prevention of crime to be proactive than reactive. To achieve the desire result, a classification model using  Gaussian Naive Bayes, Random Forest Classifier and K-Nearest Neighbors algorithm is build to categories the crime occured based on datetime and location.

## Dataset

Two datasets (train.csv and test.csv) are provided by Kaggle, but only the train dataset have used in this project. Link to access the datasets - https://www.kaggle.com/c/sf-crime/data

Data Schema is laid out below:
|Columns|Type|
|-------|----|
|Dates  | datetime64|
|Category|Object|
|Descript|Object|
|DayOfWeek|Object|
|PdDistrict|Object|
|Resolution|Object|
|Address|Object|
|X|Float64|
|Y|Float64|

The Train dataset is considerrably large dataset which consist of 878050 rows of having nearly 12 years of crime reports across all of San Francisco neighborhoods between 2003 t0 2015. The dataset consist of 9 features that describe the details are Dates, Descript,DayofWeek,PdDistrict,Resolution,Address,X,Y and Category. There are 39 categories of crime classified by SFPD in Category column and target feature for classification model and X,Y Spatial coordinates of the place where crime happened.

## Data Cleaning

There are 2323 records which are duplicate in the dataset provided, to the extent they even match datetime stamp and location coordinates as well. These duplicate records were removed so that the analysis and modelling will not be affected and also 67 records with completely wrong geo coordinates for it to belong in City of San Francisco. 5 records were updated with the correct coordinates based on their address matched and 62 records were removed, because we do not have the matching addresses.

## Modelling
### First Iteration
In this iteration, the dataset used with minimal feature engineering to build the model. Since date fields can not be used in modelling Day, DayOfWeek, Month, Year, Hour and Minute were derived from Dates field. The string fields like Address, Dates, Descript and Resolution were dropped.Using train_test_split,the Train dataset splitted into Training and Testing datasets. Once all the feature engineering work has done the model is built using Naive Bayes, Random Forest Classifier and K-Nearest Neighbors algorithm.

### Second Iteration
Since the quality of first Iteration of model is not good enough in any algorithm. More feature engineering has done by aggregating the data using AddressID and category for the different dates field derived from the first iteration model in SQL.The fields in main dataset with all the engineered fields is as follows – Dates, Category, Descript, DayOfWeek, PdDistrict, Resolution, Address, X, Y, AddressID, Dates_Year, Dates_Month, Dates_Day, Dates_Hour, Dates_Minutes, Dates_Seconds, Dates_WeekOfYear, Dates_DayOfYear, WeekOfYear_Category, DayOfYear_Category, DayOfWeek_Category, HourOfDay_Category, AddressID_Category, DayOfMonth_Category, MonthOfYear_Category, WeekOfYear_Category_Address, DayOfYear_Category_Address, DayOfWeek_Category_Address, HourOfDay_Category_Address, DayOfMonth_Category_Address and  MonthOfYear_Category_Address. With the help of all engineering field created, quality of model has increased extensively for all the different algorithms.

## Evaluation
The models Naive Bayes, Random Forest Classifier and K-Nearest Neighbors are evaluated using Log loss and Accuracy metric.

### First Iteration
Gaussian Naive Bayes - log loss -> 2.6, Accuracy -> 0.10
Random Forest Classifier - log loss -> 4.8, Accuracy -> 0.31
K-Nearest Neighbors - log loss -> 18.7, Accuracy -> 0.18

### Second Iteration
Gaussian Naive Bayes - log loss -> 3.55, Accuracy -> 0.42
Random Forest Classifier - log loss -> .15, Accuracy -> 0.98
K-Nearest Neighbors - log loss -> 3.17, Accuracy -> 0.65

Comparing the first and second iteration can conclude that Random Forest Classifier in second Iteration performed statble and effective classification model.
