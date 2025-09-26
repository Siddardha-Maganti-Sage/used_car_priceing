# What Drives the Price of a Car?
Sample exercise for What Drives the Price of a Car?
In this application, you will explore a dataset from Kaggle. The original dataset contained information on 3 million used cars. The provided dataset contains information on 426K cars to ensure speed of processing. Your goal is to understand what factors make a car more or less expensive. As a result of your analysis, you should provide clear recommendations to your client -- a used car dealership -- as to what consumers value in a used car.

## CRISP-DM Framework

To frame the task, throughout our practical applications, we will refer back to a standard process in industry for data projects called CRISP-DM. This process provides a framework for working through a data problem. Your first step in this application will be to read through a brief overview of CRISP-DM here. After reading the overview, answer the questions below.

Dataset Summary

Data set used: https://github.com/Siddardha-Maganti-Sage/coupons_accepted/blob/main/coupons_acceptance/data/coupons.csv

Jupiter Notebook link: https://github.com/Siddardha-Maganti-Sage/coupons_accepted/blob/main/coupons_acceptance/prompt_assignment.ipynb

### Business Understanding
Definition:
    We are attempting to predict the price of a user's car from a given dataset to assist the client 
    (a car dealership) with their inventory and sales.

## We will try to answer the following questions:
  * What factors most significantly impact the resale value of the car?
  * Is customer value certain attributes (features) more than others?
  * How does age and mileage increase or decrease the value?
  * Are there categories, such as model or transmission, that sell for higher prices?
    
## Success Criteria:
  * Identify key predictors of price with supporting visualizations
  * Provide recommendations to the dealership.

### Data Understanding
  * Most cars are between 5 and 20 years old
  * Mileage is right-skewed; most cars have under 200,000 miles
  * Price decreases as the age increases
  * Price decreases as the mileage increases

### Data Preparation
## Features & Categorical variables
  * Numeric Features: age, odometer
  * Categorical: condition, fuel, transmission, title_status, region, manufacture
  * We are going to use one-hot encoding, which is best for fewer unique values for columns condition, fuel, transmission, title_status & region, but for manufacturer and model, we need to use Frequency encoding ( and Target encoding)
  * Feature selection with Lasso
    
### Modeling
I will use the two models below with polynomial features to get non-linear functions
  * Linear Regression
  * Ridge Regression
I also attempted to run Random Forest, but it took a long time to execute, so I used sample data to gain some insight.

## Feature importance
Both linear and ridge models yield the same RMSE of 1.08702, with a $ value of 17,273,318.98107, without polynomial features.
Once you add polynomial features, the RMSE is reduced to 1.00329.

### Evaluation
 * Used GridSearchCV to get the best alpha values for Ridge
 * Found Ridge is underfitting
 * Tried Random Forest Regressor without polynomial functions
   Train vs Test gap still small → no overfit
 * Test score modestly improved over Ridge and RF+Poly.
 * This is less underfit than Ridge, but still not “good enough” (R² ~ 0.42 is low).
 * Used RandomizedSearchCV to get the best parameters for Random ForestRegressor

### Deployment
## Summary
  We developed models to predict the prices of used cars. After comparing Ridge Regression and Random Forests. Random Forest without polynomial features performed best with ~42% of price variation.

## Key Features to look for
  * Age & Odometer are the strongest price drivers, and (older/high-mileage cars lose value)
  * Condition, Fuel Type, Transmission, and Body Type also influence price.
  * Clean titles add value.
## Deployment Plan
  * Deliver the Random Forest Model in a pipeline that takes car details as input and outputs the estimated market price.
  * Retrain regularly with new market data.
## Limitations
  * Predictions are less accurate for luxury cars
  * Sudden market shocks (COVID), like supply chain interruptions, are not captured.
