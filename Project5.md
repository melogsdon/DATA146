# Project 5, Part I

## Setup 

After downloading and importing the anonymized dataset `persons.csv` and preprocessing the data by converting all values to `int` and filtering out the `NaN` values, I performed three different regressions (linear, Ridge, and Lasso) and computed the Mean Standard Error (MSE) or correlation coefficient (R^2) to compare the performance of each one. 

First, I used the variable `wealthC` as my target, and then I changed it to the variable `wealthI` to determine which is a better indicator of wealth prediction in the unknown West African country. 

For each regression model, I used the raw data and then standardized data to determine correlation between the features (a list of 60 different descriptive factors for people in the country, including potability of the person's water, their age and gender, weather they own a car, the type of electricity and cooking mechanisms present in the home, and more) and the target (either `wealthC` or `wealthI`). 

All of the reported correlation coefficients and MSE are from the testing data, which was used to test the models after "training" to a randomly selected subset of the data, and thus indicate the strength of the model's ability to predict unknown data. 

## Target Variable: `wealthC`

### Linear Regression

First, I performed a Linear Regression using both the raw data and standardized data. Shown below, the MSE and R^2 values indicate a strong correlation between the features and the `wealthC` target. The standardized MSE and R^2 are quite close to the raw data, indicating that standardization does not have a significant effect on the overall measure of correlation. 


|Raw Data MSE|Standardized Data MSE|
|---|---|
|0.44281|0.45205|

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.73582|0.73031|

The values of R^2 for the two datasets are similar, though not identical, and this is reflected in the correlation coefficients given by the below snippets of code as well. 

The correlation matrices were nearly identical, with small changes a few decimal places down. 

~~~~
tform_df = pd.DataFrame(data=tform_X)
tform_df['wealthC'] = y
tform_df.corr()
~~~~

~~~~
df = pd.DataFrame(data=X)
df['wealthC'] = y
df.corr()
~~~~

`tform_x` and `X` are the standardized and raw feature data, respectively, and `y` represents the target data. 

### Ridge Regression

Similarly to the linear regression model, the Ridge regression performed well with a strong correlation reflected in the R^2 value of around 0.73. The standardized data reflects a very slight improvement on the raw data, and the overall data is comparable to the linear regression model's results. 


|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.73478|0.73505|

### Lasso Regression

The Lasso regression, too, indicates a strong correlation between targets and features, and the correlation is essentially the same as the previous two models. The standardized data shows a slight improvement in correlation. 

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.73386| 0.73502 |

## Target Variable: `wealthI`

The features clearly correlation with the target variable `wealthC`, with an overall R^2 of around 0.73 across all regression models. 

Next I analyzed the same features with the same regression models with the new target variable of `wealthI`. 

### Linear Regression

The linear regression for this target variable is even more favorable than the previous. The R^2 values, again, are highly comparable and seem to indicate almost no difference between standardized and raw data. 

The correlation matrices are comparable yet again, and the features show a strong ability to predict `wealthI`. 

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.82383|0.82281|

### Ridge Regression

The Ridge regression for this target is a slight improvement on the linear regression, as shown in the chart below.

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.82463|0.82520|

### Lasso Regression

Finally, I performed a Lasso regression as in my consideration of `wealthC`, and again found that `wealthI` has a stronger correlation with the features. 

|Raw Data R^2|Standardized Data R^2|
|---|---|
|0.82522|  0.82501 |


## Analysis and Conclusions

Overall, it is clear to see that `wealthI` is a stronger measure of wealth in this anonymous West African country than `wealthC`.

<img src="wealthC_ridge.png" width="800">

 **Plot 1:**  Plot of *R^2 vs. Alpha value* for Ridge regression. Used standardized dataset of testing data for the `wealthC` target.
 
<img src="wealthI_ridge.png" width="800">

 **Plot 2:**  Plot of *R^2 vs. Alpha value* for Ridge regression. Used standardized dataset of testing data for the `wealthI` target.
 
The Ridge regression seemed overall best, because although the Lasso R^2 coefficient was slightly higher for the `wealthI` target, it was nearly identical to the Ridge coefficient. For `wealthC`, the Ridge model performed slightly better than the Lasso, and so it seems overall the best indicator of correlation between wealth and our features. Both the Lasso and the Ridge regressions performed better than the linear, though the improvement was so slightly that any of the three can be reliably utilized as a predictor. 
