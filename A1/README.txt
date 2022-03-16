******************How to reproduce the results for Assignment 1*************************

------------------Task 0: Prepare the data and libraries--------------------------------
First make sure you have the right packages installed and updated. We use the following packages:
pandas, statistics, numpy, StringIO, numpy.linalg, matplotlib.pyplot, scipy.sparse, random, sys, 
time, math, collections, sklearn.linear_model, sklearn.model_selection, sklearn.datasets, sklearn.metrics.

Next step is to import the data. We do this using the function pd.read_table(), with parameters header=None, 
encoding= 'ISO-8859-1',engine='python', sep = '::') and we name the columns 'UserID','MovieID','Rating','Timestamp'. 


------------------Task 1: Naive Approaches----------------------------------------------
We first tried to take the average rating over the entire dataset to get a feeling for the data. We then realized that we had 
to apply k-fold cross validation and take the average ranking per fold. First we got R_global. We used a random seed of 123 
and kfold split is 5 with shuffle=true. We then looped over the train and test splits and calculated the average ranking for every split.
To get the RMSE and MAE we used the scikit learn functions for MAE and RMSE. We then printed the average MAE and RMSE over the 5 k splits. 


Next we needed to find R_movie. We used the same random seed and kfold parameters. In the k-fold loop, we first groupby the movie
and calculate the average rating for each movie. Then we merge our test split with the average ranking for each movie that we just made
and we merge left on MovieID. The resulting matrix will have a lot of NA spots and these can be filled using the global average
that we calculated in the beginning. The RMSE and MAE is calculated in the same way.
We use the same procedure to find R_user except we groupby and merge on UserID.

Lastly, we needed to create a linear model, one with and one without an error term gamma. Again we set the seed to 123 and 
do a k=5 split of test and train sets. We use the function LinearRegression() and fit the data. This procedure is basically the same
for both with and without gamma, except in the case of with gamma in the Linear Regression we add the parameter fit_intercept=True
and without gamma fit_intercept=False. 


-----------------Task 2: UV decomposition------------------------------------------------
Again we use random seed 123 and set the learning rate to 0.5, number of iterations to 10 and dimension d=2. We loop over each fold and
create a pivot table to represent the larger user-item U*V matrix. We then normalize this matrix and define the user matrix and the item matrix
by initializing them filled with the value 1. Next we iterate 10 times over UV decomposition algorithm, which uses the calculation of RMSE and tries to minimize it.
With this error term, we find a prediction for the empty values in the matrix and inputs these predictions in our matrix.
We do this iteratively (in our case 10 times). We then calculate the RMSE and MAE for each iteration for each fold and print it.



----------------Task 3: Matrix Factorization---------------------------------------------
Again set seed to 123, num factors=10, num iter=75, regularization=0.05, learn rate=0.005. We set the number of hidden factors to 10. 
We made a function that we could call and that would execute matrix factorization for these given parameters.
It goes through 75 iterations to calculate the error iteratively and use regularization to avoid overfitting.





