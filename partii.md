# Project 5, Part II

## Setup 
  
In Part II, I analyze a slightly different dataset `city_persons.csv` from a larger city than before, in a West African country. After importing the data, I again preprocessed by excluding null values indicated by `NaN` and changing all of the data to the same data type by converting two of the columns to `int`. 

Whereas last time I considered both  `wealthC` and `wealthI`, this time I only analyze data using `wealthC` as the target. 

This time, my analytical focus will be clustering, to identify into which wealth class persons in the dataset fall, with three different clustering models for comparison.  

## Clustering: K-nearest neighbors

The first clustering method I tried is K-nearest neighbors (KNN), which assings classification to a particular data point according to its "k-nearest" (for some chosen integer k) neighboring points. 

The optimal k-value I found for this data was 186 neighbors, and the testing data correlation coefficient was 0.54417, indicating a moderate correlation.

KNN can be performed using "weights," which can tell KNN which characteristics to consider more than others. In this case, after testing the data without specifying a weight, I told KNN to consider distance between points and weight them using the distance (i.e. closer points would be considered more important than further points in informing a datapoint's classification). 

After adding the distance weight, the optimal k-value turned out to be 128 neighbors, and the correlatin coefficient is slightly lower than before at 0.50756, indicating that the data was slightly more reliably modelled without distance weighting.

## Clustering: Logistic Regression

- Execute a logistic regression method on the data. 
- How did this model fair in terms of accuracy compared to K-nearest neighbors?

Next, I performed a logistic regression on the dataset, after scaling the data using `StandardScaler`. 

|  Training R^2  |  Testing R^2  |
|----|----|
| 0.54979 | 0.54677 |

The logistic regression performed better than the weighted KNN model, and slightly better (though similarly) to the unweighted KNN model. 

Since the training better has a slightly higher correlation than the testing, we can see that the data is slightly overfit, but overall the values are quite close and comparable.

## Clustering: Random Forest Model

- Also test the minimum number of samples required to split an internal node with
  a range of values. 
- Also produce results for your four different estimator values by both comparing
  both standardized and non-standardized (raw) results.

Next, I executed a random forest model and ran it four times, with 100, 500, 1000, and 5000 trees. In all of these trials, I found my data was quite underfit, as the average training score was over 0.7 for each trial. 

| Trees | Testing R^2 |
| --- | ---|
| 100 | 0.48804 |
| 500 | 0.49244 |
| 1000| 0.49732 |
| 5000| 0.48902 |

The Each of these performed worse than the KNN and logistic models, so I tried standardizing the data. 

After standardization, the new chart (below) depicts data that is slightly more correlated than before, though overall very similar. 


| Trees | Testing R^2 | Scaled Testing R^2 |
| --- | ---| ----| 
| 100 | 0.48804 | 0.49195 |
| 500 | 0.49244 | 0.49927 |
| 1000| 0.49732 | 0.50122 |
| 5000| 0.48902 | 0.50220 |


## Repeat with new clusters

Repeat the previous steps after recoding the wealth classes 2 and 3 into a single outcome. Do any of your models improve? Are you able to explain why your results have changed?

## Conclusions and Analysis

Which of the models produced the best results in predicting wealth of all persons throughout the large West African capital city being described? Support your results with plots, graphs and descriptions of your code and its implementation. You are welcome to incorporate snippets to illustrate an important step, but please do not paste verbose amounts of code within your project report. Avoiding setting a seed essentially guarantees the authenticity of your results. You are welcome to provide a link in your references at the end of your (part 2) Project 5 report.

