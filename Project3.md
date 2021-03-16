## Question 1
- Train and test your target and features using a linear regression model. Describe how your model performed. 

I assigned 10 folds (splits) in my data so that out of the 715 data points, I would have 10 groups of around 71 data points. `KFold` then takes my data (Charleston asking price data) and randomly assigns the 715 data points into these ten groups. It will then iterate through and use each individual group as the testing data for the other nine (approximately 639 data points) until each fold has acted as training data nine times and testing data once. 

My model produced training and testing scores of 0.019 and -0.109, respectively. These scores indicate very poor model performance: in fact, they indicate absolutely no meaningful correlation found using this model! A "perfect" correlation score would be 1, and a good score would be closer to 1 in the range of 0 to 1 (i.e. 0.8, 0.91, etc). 

As is, the data clearly lacks predicitve ability. However, there are plenty of options to transform the data that will hopefully improve our model. The first of these is transformation

- Interpret and assess your output.

## Question 2
- Now standardize your features (again beds, baths and area) prior to training and testing with a linear regression model (also again with asking price as your target). 
- Now how did your model perform?
- What were the training and testing scores you produced? 
- How many folds did you assign when partitioning your training and testing data? 
- Interpret and assess your output.

We can use `StandardScaler()` to standardize our features and hopefully compare them more easily. Since many parts of our data are scaled differently (e.g. number of bathrooms will be on an entirely different order of magnitude than price in dollars), we might be able to improve upon our model by accounting for this difference. 

Now, the model performs marginally better than it did before. Our new training and testing scores are 0.014 and 0.069, respectively. We've lost the negative value that previously indicated simply that there was no correlation between the data we used to build our model and the data we used to test it. Now, while we still can see no strong correlation, it is slightly different and slightly more effective. 

I still used 10 folds for training and testing the data, so the only thing changed between this model and the previous is that the data has undergone a transformation. 

Overall, the model performs badly and is unable to indicate any correlation between the asking price of a house and the number of beds, baths, and size. Since the testing score is different from the training score, we can see that the model also is unable to fit to data it hasn't seen before and has no predictive power. To rectify this, we can try a ridge regression, which is often used for overfit data. 

standardize: standard scalar, transform data, not all of it (just the features, probably)


## Question 3
- Then train your dataset with the asking price as your target using a ridge regression model. 
- Now how did your model perform? What were the training and testing scores you produced? 
- Did you standardize the data? 
- Interpret and assess your output.


I used `LinearRegression()` in `sklearn` first to compare with the ridge regression model, and it yielded a correlation coefficient of 0.0188.




## Question 4
- Next, go back, train and test each of the three previous model types/specifications, but this time use the dataset charleston_act.csv (actual sale prices). 
- How did each of these three models perform after using the dataset that replaced asking price with the actual sale price? 
- What were the training and testing scores you produced? 
- Interpret and assess your output.


## Question 5
- Go back and also add the variables that indicate the zip code where each individual home is located within Charleston County, South Carolina. 
- Train and test each of the three previous model types/specifications. 
- What was the predictive power of each model?
- Interpret and assess your output.


## Question 6
- Finally, consider the model that produced the best results. Would you estimate this model as being overfit or underfit? 
- If you were working for Zillow as their chief data scientist, what action would you recommend in order to improve the predictive power of the model that produced your best results from the approximately 700 observations (716 asking / 660 actual)?
