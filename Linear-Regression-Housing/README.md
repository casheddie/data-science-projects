## Prediciting Housing Prices in Ames, Iowa using Linear Regression

---
## Executive Summary 
The goal of this project is to use a linear regression model to accurately predict the price of houses in Ames, Iowa given a set of historical sales data.  
## Table of Contents

| Item | Description | Link |
| --- | --- | --- |
| Project Code |  Technical Notebook of Code (Jupyter Notebook)| [Link](Ames-Housing-Project-Eddie-Reed.ipynb)|
| Data | Repository of datasets used in project | [Link](datasets)|
|Power Point| Slide deck of presentation| [Link](Project_2_Ames_Iowa_linear_regression_eddie_reed.pptx)|
---
## Data Collection and EDA
The data used in this project was a csv file of historical sales data of houses in Ames, Iowa.  The dataset contained 2050 observations (rows) with 81 different columns(features). 

After importing the data, I checked the file to see if there were any missing values, verified datatypes for each column and checked to see if any features could be combined.  I noticed the file had a number of null values for various cells in the different columns.  According to the data dictionary of the source data, most of the null types implied that the property did not have that particular feature.  For example, for the "fireplace Qu" column, a null value meant that the property had no fireplace.  

In all cases where null values indicated the property didn't have that particular feature, I imputed those values with an indicator that the property didn't have that feature. (e.g. "no fireplace" we imputed for the null values in the "Fireplace Qu" column)

I also noticed that a number of the columns were redundent and in those cases, I dropped the redundent columns.  Finally, I converted all categorical columns into binary values so that the model could evalute them. 

## Preprocessing and Modeling

Once the data was cleaned, I created a correlation matrix using all features and just comparied them to the sales column, since that is what I'm trying to predict. I sorted the values in descending order to determine the features which had the highest correlation on the sales price.  I narrowed down the list of features that had the most impact on sales to the following 6 features:

`features = [Overall Qual', 'Gr Liv Area', 'Garage Cars', 'Garage Area', 'Total Bsmt SF', '1st Flr SF]`

I created my X and y variables and split the data into two sets using the train/test split module in `sklearn`.  I then fit the training data using the `LinearRegression` model.

## Evaluation of the Model

After fitting the model, I calculated the r2 scoure of the training data which was 79%.  I then compared it to the r2 score of the test data set which was 72%.  Comparing these scores, model is a bit overfit.  I also calculated the cross validation score using using 5 folds and the mean of the cv scores was 78%.  

## Conclusion 

Based on the features I selected, my model would predict the the sales price of a house 72% of the time. To try to improve on this, more features could have been incorporated and also using some feature engineering could possibly increase the performance of the model.  

The model is also a little overfit with the training dataset having an r2 score of 79%. I mainly used the default values for the hyperparameters so tuning these values should yield a better performing model.  

Overall, the model does show that there is a good correlation with some of the top features in houses like overall quality, square footage, and whether the property has a garage, in predictng the sales price of a house.  
