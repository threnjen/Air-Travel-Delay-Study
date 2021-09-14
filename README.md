# Air Travel Delay Study (Module 3 Final Project)

For: Frontier Airlines

By: Jen Wadkins


## Introduction

>As the airline with the highest proportion of flight delays, Frontier Airlines has asked me to study the reasons behind flight delay, and determine what if any actions the company can take to reduce their delay impact.

## Questions

* q1?
* q2?
* q3?
* q4?

## Methodology - OSEMN

### Obtaining the Data
* Source data from Bureau of Transportation and National Weather Center
### Scrubbing/Cleaning the Data
* Clean and prepare data for model processing
### Exploring/Visualizing the Data
### Modeling the Data
* Process data with a variety of models to find the most effective model
* Provide a "realtor simulator" model to compare with machine learning model
* Demonstrate ability of model to make new predictions
### Interpreting the Data

## Table of Contents


#### [OS_dataset_cleanup.ipynb](https://github.com/threnjen/flatiron_module_03_project/blob/master/OS_dataset_cleanup.ipynb

> Project Overview
> Obtaining our Data
> Scrubbing/Cleaning our Data for OVERALL DELAY
> Scrubbing/Cleaning our Data for SPECIFIC DELAY
> Process Test Set


#### [EMN_modeling_Overall.ipynb](https://github.com/threnjen/flatiron_module_03_project/blob/master/EMN_modeling_Overall.ipynb

> Project Overview
> Exploring/Visualizing Data
> Modeling
> Model Evaluation
> Conclusions and Recommendations
> Future Work
> Explanation of Attempts - Feature Engineering/Selection
> APPENDIX


## Analysis

> ![Statistical Model Summary](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/output.png)

> Our final model utilizes a combination of continuous variables and one-hot-encoded categoricals to produce a linear regression with R^2 of 88.2% and a mean absolute error of 56k. I tried several different transformations including polynomial features, mean target encoding, lower-granularity binning, and median rank as a continuous, and ALL of these efforts resulted in a lower R^2 and higher mean absolute error, leading to a final decision to one-hot encode all 70 zip codes individually. Similar efforts on other categoricals such as age and month sold also did not improve the model over one-hot encoding. This resulted in the greatest accuracy despite a model that is more "messy" with a large number of features.

> Features were selected using the sklean "Recursive Feature Elimination with Cross Validation" function, or RFECV. RFECV uses cross-validation and begins the model with all features, then eliminates the weakest feature and scores the model again, using cv with each iteration. At the end it returns the model with the feature set that produced the highest score on the cv. In the case of price predictions I used mean absolute error as my preferred scoring metric. Then, starting with the features recommended by RFECV, I ran the model again through a forward-backward feature selector, which starts with zero features and iteratively adds and subtracts features until all features have a p-value under the threshold (in this case .05). 

> Almost all included features had p-values so low that the probability that these features are influencing the price by random chance is near zero. Our highest included p-value, zipcode 98003, has only a .3% chance of having influenced prices by random chance.

> 88.2% of our variation in price can be explained by our model variables. Our equal R^2 and adjusted R^2 tells us that all of our features are contributing to our model. Adjusted R^2 penalizes the R^2 formula based on number of variables, so a same score tells us that our variables are all contributors.

> F-statistic and Prob(F-statistic) tell us if our variable group as a whole is statistically significant. The null hypothesis is a model with no variables (only intercept). Our prob(f-statistic) evaluates the chance that our null hypothesis is true and our variables have no effect. On our model this chance is so low that it's functionally 0. F-statistic is evaluating all of the coefficients used together, so p-value of individual coefficients is still important. So this number tells us that our MODEL is significant without telling us if any individual feature is significant.

> Omnibus and prob(omnibus) tell us that our residuals are not normally distributed. We want to see a value close to 0 for Omnibus, and a value close to 1 for Prob(Omnibus). Neither of these things is the case. We saw heteroscedasticity on the residuals for all of our model types that we tried. All of our models seem to perform well at lower prices and then variance increases as price increases. This was true on both linear and nonlinear approaches such as decision trees.
>![Residuals](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/residuals.png)

> Our data is skewed slightly left. Our data has high kurtosis which implies tighter grouping of our residuals around zero and fewer outliers, which implies a fitted model.

> Durbin Watson is a measure of homoscedasticity - an even distribution of errors. We are showing slight heteroscedasticity because we'd like to see this number between 1 and 2. We saw the heteroscedasticity in the residuals.

> Our low condition number implies no multicollinearity with our features.

> Overall our characteristics are mediocre. Our high omnibus and above 2 Durbin-Watson are problematic. But no better model was found to correct for the heteroscedasticity.

## Conclusion

#### Q1?
> Answer 
>![Total Price per Total Square Footage, by Grade](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/pr_grade.png)

>more answer

#### Q2?
> Answer

#### Q3?
>Answer

>![Figure 1 - Housing Sales in King County by Location](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/comps_plat.png)

>more answer

#### Q4?

>Answer


## Recommendations for Future Work

> 


## Presentation
[Video - Data Science Module 2 Project](https://youtu.be/vsyFdHGtmqM)

[PDF of Presentation](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/mod_2_project.pdf)





References:
* https://machinelearningmastery.com/threshold-moving-for-imbalanced-classification/
* https://stackoverflow.com/questions/19984957/scikit-learn-predict-default-threshold
* https://towardsdatascience.com/how-to-add-decision-threshold-tuning-to-your-end-to-end-ml-pipelines-7077b82b71a
* https://www.fharrell.com/post/classification/
* https://machinelearningmastery.com/out-of-fold-predictions-in-machine-learning/
* https://www.kaggle.com/arthurtok/introduction-to-ensembling-stacking-in-python
* https://bradleyboehmke.github.io/HOML/stacking.html
* https://www.kdnuggets.com/2017/02/stacking-models-imropved-predictions.html
* https://machinelearningmastery.com/stacking-ensemble-machine-learning-with-python/
