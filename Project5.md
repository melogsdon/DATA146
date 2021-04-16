# Project 5, Part I

## Setup 

Download the anonymized dataset describing persons.csv from a West African county and import it into your PyCharm project workspace (right click and download from the above link or you can also find the data pinned to the slack channel). First set the variable wealthC as your target. It is not necessary to set a seed.

## Linear Regression



#### Standardization
Perform a linear regression and compute the MSE. Standardize the features and again computer the MSE. 

|Raw Data MSE|Standardized Data MSE|
|---|---|
|0.44281|0.452045|

Compare the coefficients from each of the two models and describe how they have changed.



### Ridge Regression

Run a ridge regression and report your best results.

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.44281|0.452045|

### Lasso Regression

Run a lasso regression and report your best results.

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.44281|0.452045|

### Change of Target Variable

Repeat the previous steps using the variable wealthI as your target.

### Analysis and Conclusions

Which of the models produced the best results in predicting wealth of all persons throughout the smaller West African country being described? Support your results with plots, graphs and descriptions of your code and its implementation. 

You are welcome to incorporate snippets to illustrate an important step, but please do not paste verbose amounts of code within your project report. Alternatively, you are welcome to provide a link in your references at the end of your (part 1) Project 5 report.
