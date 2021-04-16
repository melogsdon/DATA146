# Project 5, Part I

## Setup 

Download the anonymized dataset describing persons.csv from a West African county and import it into your PyCharm project workspace (right click and download from the above link or you can also find the data pinned to the slack channel). First set the variable wealthC as your target. It is not necessary to set a seed.

## Linear Regression

Perform a linear regression and compute the MSE. Standardize the features and again computer the MSE. 

|Raw Data MSE|Standardized Data MSE|
|---|---|
|0.44281|0.45205|

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.73582|0.73031|

Compare the coefficients from each of the two models and describe how they have changed.



## Ridge Regression

Run a ridge regression and report your best results.

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.73478|0.73505|

## Lasso Regression

Run a lasso regression and report your best results.

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.73386|   |

## Change of Target Variable

Repeat the previous steps using the variable wealthI as your target.

#### Linear Regression

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.82583|0.82281|

#### Ridge Regression

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.82463|0.82520|

#### Lasso Regression

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.82522|  0.82501 |


### Analysis and Conclusions

Which of the models produced the best results in predicting wealth of all persons throughout the smaller West African country being described? Support your results with plots, graphs and descriptions of your code and its implementation. 

You are welcome to incorporate snippets to illustrate an important step, but please do not paste verbose amounts of code within your project report. Alternatively, you are welcome to provide a link in your references at the end of your (part 1) Project 5 report.
