# AimesIowaHousingPricePredictions
Linear Regression to predict house sale prices in Ames Iowa

<h2>The Data</h2>
This is a very detailed dataset containing 79 features describing sold houses in great detail.  My goal was to develop a model for predicting house prices

<h2>Approach</h2>
<ul>
<li>started with a simple baseline model that used house quality ranking to predict sale price and achieved better than average accuracy (R2=.64) (64% of the variability in pirces can be explained by that feature alone)</li>
<li>used SKLearnPandas to clean up and organize the data</li>
 <ul>
  <li>converted categorical columns to dummies</li>
  <li>imputed missing values</li>
  </ul>
<li> next ran a simple Linear Regression using all the features included in the data set and achieved reasonable accuracy (certainly better than the baseline mode)</li>
<li>Used feature selection to whittle down number of features.  Compared results of feature selection using KBest, Lasso and X -- KBest with 100-125 features generally performed the best</li>
<li>The residuals plot showed that the predictions were particularly off for higher priced houses.  EDA had shown that there were two potential outliers in the training data = large houses that sold for relatively cheap.  Removing those from the dataset improved the R2 score to .9 </li>
<li>Originally just binarized all categoricial features, but some were ranked features (i.e. po, fair, good, excellent condition).  So converted those columns to numeric rankings.  The R2 score diminished slightly at this point</li>
<li>Became worried that most important predictors (such as overall quality and square footage, both of which have a very high correlation with sale price) were becoming lost in the noise of all the features. So added Polynomial features on the top correlated features (tried 2nd and 3rd degree - 2nd had better results).  This increased the R2 score back up to .90</li>
<li>Noticed on residual plot that the model was still consistently poor at predicting the higher priced houses. It showed signs of heteroscedasticity, with bigger errors for higher house prices. So tried adding a log transform on house price to counteract this </li>
<li>Tried KNeighborsRegression in case it was better able to handle the right-skew of sale price, but it performed somewhat worse</li>
<li>returned to LinearREgression and played with removing some additional features</li>
</ul>


<h2>Results</h2>

Finally settled on using model that used:
<ul>
<li>KBest to pick the top 125 columns</li>
<li>Linear Regression</li>
<li>reduced basic features</li>
<li>polynomial features on top 10 numeric columns correlated with sale price</li>
<li>log transform of house price</li>
</ul>
