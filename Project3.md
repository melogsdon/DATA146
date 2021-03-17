# Project 3

Using housing data from Charleston, South Carolina, let's build a model that will attempt to describe some correlation between housing cost (both in actual cost and asking price) and various housing characteristics (size, amenities, location). 

## Linear Regression

The Charleston asking price data set `charleston_ask.csv` contains 715 data points, each representing a house sale in any of the counties in Charleston. In order to separate this data into "training" and "testing" sections, we will use an API called KFold. Training data is set aside from a data set for actual model building, and testing data is used to test the model's predictive power. We will use a correlation coefficient to determine how well these models correspond to a linear regression. 

I asigned ten folds (splits) in the data so that out of 715 data points, we have 10 groups of around 71 data points. `KFold` then takes my data (Charleston asking price data) and randomly assigns the 715 data points into these ten groups. It will then iterate through and use each individual group as the testing data for the other nine (approximately 639 data points) until each fold has acted as training data nine times and testing data once. 

My model produced training and testing scores of 0.019 and -0.109, respectively. These scores indicate very poor model performance: in fact, they indicate absolutely no meaningful correlation found using this model! A "perfect" correlation score would be 1, and a good score would be closer to 1 in the range of 0 to 1 (i.e. 0.8, 0.91, etc). 

As is, the data clearly lacks predicitve ability. However, there are plenty of options to transform the data that will hopefully improve our model. The first of these is transformation

#### Charleston Asking Price: Models Summary
| Model | Description | Internal Validity | External Validity |
| --- | ---- | ------ | ---- |
|Linear Regression| Fit to raw data |0.019|-0.109|

## Standardizing Data for a Linear Regression

We can use `StandardScaler()` to standardize our features and hopefully compare them more easily. Since many parts of our data are scaled differently (e.g. number of bathrooms will be on an entirely different order of magnitude than price in dollars), we might be able to improve upon our model by accounting for this difference. 

Now, the model performs marginally better than it did before. Our new training and testing scores are 0.014 and 0.069, respectively. We've lost the negative value that previously indicated simply that there was no correlation between the data we used to build our model and the data we used to test it. Now, while we still can see no strong correlation, it is slightly different and slightly more effective. 

I still used 10 folds for training and testing the data, so the only thing changed between this model and the previous is that the data has undergone a transformation. 

Overall, the model performs badly and is unable to indicate any correlation between the asking price of a house and the number of beds, baths, and size. Since the testing score is different from the training score, we can see that the model also is unable to fit to data it hasn't seen before and has no predictive power. To rectify this, we can try a ridge regression, which is often used for overfit data. 

#### Charleston Asking Price: Models Summary
| Model | Description | Internal Validity | External Validity |
| --- | ---- | ------ | ---- |
|Initial Regression | Linear regression fit to raw data |0.019|-0.109|
|Standardized Features| Linear regression fit to data transformed with `StandardScaler`|0.014|0.069|


## Ridge Regression

Since our standardized data left much to be desired, let's try a new method for building our model. Again, we will scale the data using  `StandardScaler()` since this seemed to help a bit, and try a new regression technique call a ridge regression. This time, it yields a training correlation coefficient of 0.019 and a testing correlation coefficient of 0.016. This is much better than the others, as the correlations are closer together (and, of course, the testing coefficient is non-negative!), though they are still extremely small and are unable to show any meaningful connection in our data.

Overall, it seems that the models are still unable to show a meaningful connection in the data.

#### Charleston Asking Price: Models Summary
| Model | Description | Internal Validity | External Validity |
| --- | ---- | ------ | ---- |
|Initial Regression | Linear regression fit to raw data |0.019|-0.109|
|Standardized Features| Linear regression fit to data transformed with `StandardScaler`|0.014|0.069|
|Ridge Regression|Ridge regression fit to transformed data|0.019|0.016|



## Applying all previous methods to `charleston_act.csv`

Since house asking price seems to not rely very convincingly on the number of beds, baths, and square feet in a house, let's see if the problem is with the asking price. We can use a new data set now, `charleston_act.csv` which contains the actual sale price of Charleston homes rather than the asking price. Since the asking price is determined by the homeowner and the sale price is determined by the homeowner and the buyer as well as the appraisal, we might expect that the actual price is more reflective of the home's value than the asking.

If we go back and apply each of the previous models (Linear, Transformed Linear, and Ridge) to the asking price, we can see almost no correlation at all. In fact, it seems to be getting worse! Clearly the problem lies not with the asking price, so let's try looking at more of the data we have available to us. So far we've ignored the location data and only focused on the attributes inside the house. 


#### Charleston Actual Price: Models Summary
| Model | Description | Internal Validity | External Validity |
| --- | ---- | ------ | ---- |
|Linear Regression| Fit to raw data |0.004|-0.021|
|Transformed Linear Regression|Linear regression fit to data transformed with `StandardScaler`|0.005|-0.013|
|Ridge Regression| Transformed data with a ridge regression|0.004|-0.001|


## Question 5
- Go back and also add the variables that indicate the zip code where each individual home is located within Charleston County, South Carolina. 
- Train and test each of the three previous model types/specifications. 
- What was the predictive power of each model?
- Interpret and assess your output.

If we consider the simple addition of location to our list of features, we see an improvement in the training data for all three models. Unfortunately, the improvement is slight and hardly indicates a strong correlation between our target and our features. 

However, we can see that adding the zip codes improves the data the most in the ridge regression, where the correlation coefficients are now 0.057 and 0.051 for training and testing, respectively. Though the coefficients are small, they are higher than the others we've seen and they're also close together, indicating some consistency at the very least. 

The predictive power of all of these models are weak, but the strongest is the ridge regresion for the data set including the houses' actual prices and locations.  

#### Charleston Actual Price by Location: Models Summary
| Model | Description | Internal Validity | External Validity |
| --- | ---- | ------ | ---- |
|Linear Regression| Fit to raw data |0.056|-0.05|
|Transformed Linear Regression|Linear regression fit to data transformed with `StandardScaler`|0.061|-0.004|
|Ridge Regression| Transformed data with a ridge regression|0.057|0.051|


## Question 6
- If you were working for Zillow as their chief data scientist, what action would you recommend in order to improve the predictive power of the model that produced your best results from the approximately 700 observations (716 asking / 660 actual)?

The model with the best results was the ridge regression on the complete data set (including the area code data) from the Charleston actual sale price data set. Since, in this particular model, the correlation coefficient is higher in the training data than in the testing data, we would say that the data is overfit. Our model is stronger in its ability to describe our training data than it is to predict new data, indicating that it fits the training data too closely. 


