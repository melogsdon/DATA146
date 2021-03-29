## Midterm Corrections

### Setup

Import the libraries you will need.
~~~~
from sklearn.datasets import fetch_california_housing
import pandas as pd
import numpy as np
from sklearn.linear_model import LinearRegression
import matplotlib
import matplotlib.pyplot as plt
from sklearn.model_selection import KFold
from sklearn.preprocessing import StandardScaler
~~~~

Create your DoKFold
~~~~
def DoKFold(model, x, y, k, standardize=False, random_state = 146):
    import numpy as np
    from sklearn.model_selection import KFold
    kf = KFold(n_splits=k, shuffle=True, random_state=random_state)

    if standardize:
        from sklearn.preprocessing import StandardScaler as SS
        ss = SS()

    tr_scores = []
    te_scores = []

    mse_train = 0
    mse_test = 0

    for idxTrain,idxTest in kf.split(x):
        xtrain = x[idxTrain,:]
        xtest = x[idxTest,:]
        ytrain = y[idxTrain]
        ytest = y[idxTest]              
        if standardize:
            xtrain = ss.fit_transform(xtrain)
            xtest = ss.transform(xtest)
        model.fit(xtrain,ytrain)
        tr_scores.append(model.score(xtrain,ytrain))
        te_scores.append(model.score(xtest,ytest))
        
    tr_scores = np.mean(tr_scores)
    te_scores = np.mean(te_scores)
        
    train_pred = model.predict(xtrain)
    test_pred = model.predict(xtest)
    tr_total = 0
    te_total = 0
    n = len(train_pred)
    m = len(test_pred)
        
    for i in range(0,n):
        diff = (ytrain[i] - train_pred[i])
        diff_sq = diff**2
        tr_total += diff_sq
    mse_train = tr_total/n
        
    for i in range(0,m):
        diff = (ytest[i] - test_pred[i])
        diff_sq = diff**2
        te_total += diff_sq
    mse_test = te_total/m
        
    return tr_scores,te_scores,mse_train,mse_test
~~~~

Import the California Housing data

~~~~
data = fetch_california_housing()
x = data.data
x_names = data.feature_names
x_df = pd.DataFrame(data=x, columns=x_names)

y=data.target

xy_df = x_df.copy()
xy_df['Target'] = y
~~~~

### Question 15
#### Which of the below features is most strongly correlated with the target?
##### MedInc (median income)
##### AveRooms (average number of rooms)
##### AveBedrms (average number of bedrooms)
##### HouseAg (average house age)

~~~~
xy_df.corr()
~~~~

The above command reveals, in the 'Target' columns, that MedInc is most strongly correlated with the target as its correlation coefficient is largest.

### Question 16
#### If the features are standardized, the correlations from the previous question do not change.

~~~~
ss = StandardScaler()
tform_x = ss.fit_transform(x)

tform_df = pd.DataFrame(data=tform_x, columns=x_names)
tform_df['Target']=y

tform_df.corr()
~~~~

The correlations are exactly the same as before.

### Question 17
#### If we were to perform a linear regression using only the feature identified in question 15, what would be the coefficient of determination? Enter your answer to two decimal places, for example: 0.12

~~~~
ans = (0.688075**2)
print(ans)
~~~~

Rounded to two decimal places, this is 0.47. 

### Question 18
#### Perform a linear regression on standardized data.
#### What is the correlation coefficient of the testing data?

~~~~
lin_reg = LinearRegression()
tr_scores,te_scores,mse_train,mse_test = DoKFold(lin_reg, tform_x, y, k=20, standardize=True, random_state=146)

print(np.mean(tr_scores), np.mean(te_scores))
print(np.mean(mse_train), np.mean(mse_test))
~~~~

Output: 
0.6063019182717753 0.6019800920504694
0.5224239582328265 0.5605458408715165

The testing coefficient is 0.60198.

### Question 19
#### Next, try a Ridge regression with the given parameters.

~~~~
from sklearn.linear_model import Ridge, Lasso

rid_range = np.linspace(20,30,101)

rid_avg_tr_score = []
rid_avg_te_score = []

rid_tr_mse = []
rid_te_mse = []

for a in rid_range:
    rid_reg = Ridge(alpha=a)
    train_scores, test_scores, mse_train, mse_test = DoKFold(rid_reg, x, y, k=20, standardize=True)
    rid_avg_tr_score.append(np.mean(train_scores))
    rid_avg_te_score.append(np.mean(test_scores))
    rid_tr_mse.append(np.mean(mse_train))
    rid_te_mse.append(np.mean(mse_test))

idx = np.argmax(rid_avg_te_score)
#
print('Alpha max: ', rid_range[idx], 'Train max: ', rid_avg_tr_score[idx], 'Test max: ', rid_avg_te_score[idx], 'Train MSE: ', rid_tr_mse[idx], 'Test MSE: ', rid_te_mse[idx])
~~~~

Output:
Alpha max:  25.8 
Train max:  0.6062707743487987 
Test max:  0.602011168741859 
Train MSE:  0.5224653779415789 
Test MSE:  0.560803373017799

### Question 20
#### Next, try a Lasso regression with the given parameters.

~~~~
las_range = np.linspace(0.001,0.003,101)

avg_tr_score = []
avg_te_score = []

rid_tr_mse = []
rid_te_mse = []

for a in las_range:
    las = Lasso(alpha=a)
    train_scores, test_scores, mse_train, mse_test = DoKFold(las, x, y, k=20, standardize=True)
    avg_tr_score.append(np.mean(train_scores))
    avg_te_score.append(np.mean(test_scores))
    rid_tr_mse.append(np.mean(mse_train))
    rid_te_mse.append(np.mean(mse_test))

idx = np.argmax(avg_te_score)
#
print('Alpha max: ', las_range[idx], 'Train max: ', avg_tr_score[idx], 'Test max: ', avg_te_score[idx], 'Train MSE: ', rid_tr_mse[idx], 'Test MSE: ', rid_te_mse[idx])
~~~~

Output:
Alpha max:  0.00186
Train max:  0.6061563795668891
Test max:  0.6021329052825213 
Train MSE:  0.5226201002196856 
Test MSE:  0.5614601136061196

### Question 21
#### Which of the three models estimates the smallest coefficient for the variable that is least correlated?

~~~~
y=data.target

least_corr = 'AveBedrms'
idx = xy_df.columns.get_loc(least_corr)

lin = lin_reg.fit(tform_x, y)
las = Lasso(alpha=0.00186)
las.fit(tform_x,y)
rid = Ridge(alpha=25.8)
rid.fit(tform_x,y)

print('Ridge coef: ', rid.coef_[idx])
print('Lasso coef: ', las.coef_[idx])
print('Linear coef: ',lin.coef_[idx])
~~~~

Output:
Ridge coef:  0.3012752123596445
Lasso coef:  0.2803974316329972
Linear coef:  0.3056962298043105

### Question 22
#### Which of the models estimates the smallest coefficient for the variable that was most correlated?

~~~~
most_corr = 'MedInc'
idx = xy_df.columns.get_loc(most_corr)

lin = lin_reg.fit(tform_x, y)
las = Lasso(alpha=0.00186)
las.fit(tform_x,y)
rid = Ridge(alpha=25.8)
rid.fit(tform_x,y)

print('Ridge coef: ', rid.coef_[idx])
print('Lasso coef: ', las.coef_[idx])
print('Linear coef: ',lin.coef_[idx])
~~~~

Output:
Ridge coef:  0.8288892465528167
Lasso coef:  0.8200140807502059
Linear coef:  0.8296193042804506

### Question 23
#### If we had looked at MSE instead of R2 when doing our Ridge regression would we have determined the same optimal value for alpha, or something different?

~~~~
rid_range = np.linspace(20,30,101)

rid_avg_tr_score = []
rid_avg_te_score = []

rid_tr_mse = []
rid_te_mse = []

for a in rid_range:
    rid_reg = Ridge(alpha=a)
    train_scores, test_scores, mse_train, mse_test = DoKFold(rid_reg, x, y, k=20, standardize=True)
    rid_avg_tr_score.append(np.mean(train_scores))
    rid_avg_te_score.append(np.mean(test_scores))
    rid_tr_mse.append(np.mean(mse_train))
    rid_te_mse.append(np.mean(mse_test))

idx = np.argmin(rid_tr_mse)
print('Alpha max: ', format(rid_range[idx], '.5f'), 'Train max: ', rid_avg_tr_score[idx], 'Test max: ', rid_avg_te_score[idx], 'Train MSE: ', rid_tr_mse[idx], 'Test MSE: ', rid_te_mse[idx]
~~~~

We get a different value of alpha. 

### Question 24
#### If we had looked at MSE instead of R2 when doing our Ridge regression would we have determined the same optimal value for alpha, or something different?

~~~~
las_range = np.linspace(0.001,0.003,101)

avg_tr_score = []
avg_te_score = []

las_tr_mse = []
las_te_mse = []

for a in las_range:
    las = Lasso(alpha=a)
    train_scores, test_scores, mse_train, mse_test = DoKFold(las, x, y, k=20, standardize=True)
    avg_tr_score.append(np.mean(train_scores))
    avg_te_score.append(np.mean(test_scores))
    las_tr_mse.append(np.mean(mse_train))
    las_te_mse.append(np.mean(mse_test))

idx = np.argmin(las_tr_mse)
print('Alpha max: ', format(las_range[idx],'.5f'), 'Train max: ', avg_tr_score[idx], 'Test max: ', avg_te_score[idx], 'Train MSE: ', rid_tr_mse[idx], 'Test MSE: ', rid_te_mse[idx])
~~~~












