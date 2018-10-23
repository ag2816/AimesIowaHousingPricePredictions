# AimesIowaHousingPricePredictions
Linear Regression to predict house sale prices in Aimes Iowa

<h2>The Data</h2>
* very detailed dataset containing 

<h2>Approach</h2>
* started with a simple baseline model that used house quality ranking to predict sale price and achieved better than average accuracy (R2=.64) (64% of the variability in pirces can be explained by that feature alone)
* used SKLearnPandas to clean up and organize the data
  * converted categorical columns to dummies
  * imputed missing values
* next ran a simple Linear Regression using all the features included in the data set and achieved reasonable accuracy (certainly better than the baseline mode)
* used feature selection to whittle down number of features (generally KBest was the best feature selection, although Lasso often worked well too. Generally, it helped to remove about half the features)
Next removed two outliers from the training dataframe (these were large houses that sold for relatively cheap)
changed from treating ranked features (i.e. po, fair, good, excellent condition) to numeric rankings
Became worried that most importand predictors (such as overall quality and square footage, both of which have a very high correlation with sale price were becoming lost in the noise of all the features. So added Polynomial features on the top correlated features (tried 2nd and 3rd degree - 2nd had better results)
noticed on residual plot that the model was consistently poor at predicting the higher priced houses. It showed signs of heteroscedasticity, with bigger errors for higher house prices. So tried adding a log transform on house price to counteract this -- it did help
Tried KNeighborsRegression in case it was better able to handle the right-skew of sale price, but it performed somewhat worse
returned to LinearREgression and played with removing some additional features



<h2>Results</h2>
finally settled on using model that used:
KBest to pick the top 125 columns
LInear Regression
reduced basic features
polynomial features on top 10 numeric columns correlated with sale price
log transform of house price
