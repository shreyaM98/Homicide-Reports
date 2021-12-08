# Homicide Reports

## Introduction


## Data and Data Cleaning

The original dataset was based on homicide reports from 1980-2014 from Kaggle. (<a href="https://www.kaggle.com/murderaccountability/homicide-reports"> Link to Kaggle Dataset </a> ) This dataset had 24 total columns listed below and each row detailed a homicide including information such as victim and perpetrator descriptions (i.e. age, race, ethnicity) and details about the murder itself (solved status, weapon type, location). While the Kaggle forum proposed interesting questions about predicting serial killers, our team wanted to take a more broad look at the state murder rates, so a lot of cleaning and synthesizing of the data needed to be done. 

| Categorical Columns  | Numeric Columns |
| ------------- | ------------- |
| Agency Code*  | Incident* |
| Agency Name*  | Victim Age |
| Agency Type | Perpetrator Age  |
|City | Victim Count  |
| State  | Perpetrator Count  |
| Year  |   |
| Month  |   |
| Crime Type  |   |
| Crime Solved  |   |
| Victim Sex |   |
| Victim Race  |   |
| Victim Ethinicity  |  |
| Perpetrator Sex|   |
| Perpetrator Race  |   |
| Perpetrator Ethincity  |   |
| Relationship  |   |
| Weapon  |   |
| Record Source |  |


The dataset was reorganized such that each row was a yearly summary for a singular state. The columns from the original dataset, excluding those with an asterisk , were cleaned to create summary statistics for a given state each year. A total crime count and total city with crime count were the first two values calculated.  For any categorical columns, a rate and count were calculated for each of the possible values of the column. Rates were calculated by dividing the count for a given value by the total crime count for that row. Relationships were ultimately grouped into more general relationship types to help reduce the total number of columns. Those groupings can be seen in the table below. For any numeric columns, the minimum, maximum, and average value was calculated. While this dataset was quite clean, any numeric values that were unknown were set to 0, thus skewing any of the numeric values. 

| New Relationship Type  | Original Relationship Types |
| ------------- | ------------- |
| Friend  | Acquaintance, Friend, Neighbor, Employer, Employee |
| Stranger  | Unknown, Stranger |
| Spoouse | Wife, Ex-Husband, Husband, Ex-Wife, Common-Law Husband, Common-Law Wife  |
| Dating | Girlfriend, Boyfriend, Boyfriend/Girlfriend |
| Sibling  | Brother, Sister  |
| Child  | Stepdaughter, Son, Daughter, Stepson |
| Parent  | Father, Mother, Stepfather, Stepmother |
| Other Family  | Family, In-Law |

After calculating all of the summary statistics based on the original dataset, we still needed to calculate crime rate and whether a state was in the top ten states for that year. A second dataset was uploaded, the Historical State Populations (1900-2017) dataset from Kaggle. (<a href="https://www.kaggle.com/murderaccountability/homicide-reports"> Link to Formula Source </a>) Using this dataset we were able to calculate each states homicide crime rate using the formula: 

<img src="equations.PNG" class="inline" class="center" />

Once these crime rates were calculated, the top ten states with the highest homicide crime rate were calculated for each year and noted in the appropriate columns. Since we want to use one year’s date to predict the next year’s crime rate and top ten status, two new columns were added to detail this information. Lastly, after all other data cleaning was done, the state column was one-hot encoded to create 51 new columns (as we were including the District of Columbia) and years were normalized to start at 1. 


In total, our new dataset had data for the years 1980 to 2013, with 2014 ultimately being ignored due to lack of homicide crime rates for 2015. In total, the data frame had 159 summary statistic columns, 210 including the additional state one-hot encoding columns and 2 prediction columns. This final dataset was split into a testing dataset, which would also be used for validation sets, and a testing set. The training set included data from years 1980 - 2008 (~85%) and the testing set included data from years 2009 – 2013 (~15%). 


## Regression Predictions 

### Linear Regression

### Time Series

### Neural Networks



## Classification Predictions

### K-Nearest Neighbors


### Logistic Regression


### Decision Trees and Random Forrests

Next, decision trees and random forrests were implimented. In both cases, the trees were fit with both gini and entropy as the criterion methods. For decision trees methods, we ran numerical tests on finding the best ccp_alpha value and max depth value to fit various trees. The parameter ccp_alpha finds the weakest nodes and prunes those nodes first versus just pruning any node beyond the max depth set with the other parameter. These paramters were optimized under both gini and entropy criterion methods. Below are the results from all of the decision trees. From the results, the highest accuracy was given by the optimal max depth tree using entropy. This tree also had the best F1 score and was on the higher end of precision and recall scores. As seen in the tree image below, the max depth for this tree was only 3. 

| Tree Type | Accuracy | F1 Score | Precision | Recall |
| ------------- | ------------- | ------------- | ------------- |------------- |
| Basic (Gini) | 0.8627 | 0.64 | 0.72 | 0.58 |
| Basic (Entropy) | 0.9745 | 0.92 | 0.89 | 0.95 |
| Optimal ccp_alpha (Gini) | 0.8588 | 0.92 | 0.88 | 0.96 |
| Optimal ccp_alpha (Entropy) | 0.8510 | 0.92 | 0.88 | 0.96 |
| Optimal Max Depth (Gini) | 0.0.8631 | 0.91 | 0.86 | 0.96 |
| Optimal Max Depth (Entropy) | 0.9137 | 0.95 | 0.94 | 0.95 |


<img src="Best_tree.PNG" class="inline" class="center" />


| Forrest Type | Accuracy | F1 Score | Precision | Recall |
| ------------- | ------------- | ------------- | ------------- |------------- |
| Basic (Gini) | 0.8706 | 0.92 | 0.88 | 0.98 |
| Basic (Entropy) | 0.8745 | 0.93 | 0.88 | 0.97 |
| Optimal Estimators (Gini) | 0.8588 | 0.92 | 0.87 | 0.98 |
| Optimal Estimators (Entropy) | 0.8627 | 0.92 | 0.87 | 0.98 |




### Support Vector Machines


## Ensemble Predictions



## Conclusion
