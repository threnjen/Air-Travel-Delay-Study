# Air Travel Delay Study (Module 3 Final Project)

For: Federal Bureau of Transportation

By: Jen Wadkins


## Introduction

> The Federal Bureau of Transportation has requested a report on if flight delay can be anticipated with their current collection metrics, with a goal of providing proper informational resources to individual carriers to assist in their reduction of delays.

## Skills Presented

* Data Cleaning
* Exploratory Data Analyis
* Data Visualization
* Feature Selection and Engineering
* Model Selection and Tuning

## Questions

* Can we anticipate a delay with the Bureau's current collection metrics?
* Given a delay, can we predict why the delay occurred?
* With this information in hand - can the BTS provide resources to help reduce delay?


## Methodology - OSEMN

### Obtaining the Data
* Source data from Bureau of Transportation and National Centers for Environmental Information
### Scrubbing/Cleaning the Data
* Clean and prepare data for model processing
### Exploring/Visualizing the Data
* Study reasons underlying delay
* Visualize relationships between features
### Modeling the Data
* Process data with a variety of models to find the most effective model
* Demonstrate ability of model to make new predictions
### Interpreting the Data
* Understand and describe the results

## Table of Contents


#### [OS_dataset_cleanup.ipynb](https://github.com/threnjen/flatiron_module_03_project/blob/master/OS_dataset_cleanup.ipynb

* Project Overview
* Obtaining our Data
* Scrubbing/Cleaning our Data for OVERALL DELAY
* Scrubbing/Cleaning our Data for SPECIFIC DELAY
* Process Test Set


#### [EMN_modeling_Overall.ipynb](https://github.com/threnjen/flatiron_module_03_project/blob/master/EMN_modeling_Overall.ipynb
* **Project Overview**
    * OSEMN Plan
    * Package Imports    
    * Notebook Functions

* **Exploring/Visualizing Data**
    * Visualizations by feature
    * Correlations

* **Modeling**
    * Preprocessing
    * Spot Check Baseline Algorithms
    * Spot Check Imbalanced Algorithms
    * Feature Selection
    * Evaluate Spot Checks
    * Tuned Base Models
    * Tuned Stacked Model

* **Model Evaluation**

* **Conclusions and Recommendations**

* **APPENDIX**
    * Hyperparameter Tuning

#### [EMN_modeling_Specific_Delay.ipynb](https://github.com/threnjen/flatiron_module_03_project/blob/master/EMN_modeling_Specific_Delay.ipynb

* Project Overview
* Exploring/Visualizing Data
* Modeling
* Model Evaluation


## Analysis

### Scoring Reasoning
We score our model on F1 score rather than Accuracy. Accuracy is very easy to reach on this data - the model simply predicts very few delays when tuning and scoring on Accuracy. We would use accuracy if all classes are equally important. It's possible that the cost of a false negative is low in this instance, but the entire purpose of the model is to understand and predict a delay, so we will consider the cost of false negatives to be high.

Since want to minimize the number of False Negatives, we use F1-Score instead, which is the harmonic mean of precision (reduce false positives where a delay was predicted and was not) and recall (reduce false negatives where a delay was not predicted and was delayed). This overall gives us a better measure of the incorrect classifications.

F1 is also considered a better metric when the set is highly imbalanced, for the simple reason that if based on Accuracy, the model may simply always predict for the majority class. In our situation, with a 80/20 imbalance, the model could easily achieve 80% accuracy by simply always prediction that a flight will not be delayed. This is not a useful prediction for us.

### Results
Ultimately, predictive quality of the model was very low.

**Accuracy 62.3% - how many overall predictions were correct?** We did NOT optimize accuracy, because our data is heavily imbalanced. With imbalanced datasets, the highest accuracy can often be obtained by largely ignoring the minority class. This results in very high accuracy, but low Precision, Recall, and F1.

**Precision 20.3% - Out of the delays we predicted, how many were correct?** Our precision was very low, as the model predicted far more delays than were actually true. We minimize Precision when the cost of False Positives are high. Our cost of False Positives here wasn't that high, so we did not minimuze Precision directly.

**Recall 58.6% - Out of all ACTUAL delays, how many did we predict?** We predicted just over half of the actual delays. Recall minimizes False Negatives. We did want to predict as many actual delays as possible.

**F1 30.2% - How was our combined Precision and Recall?** Our F1 is very low. F1 represents the harmonic mean of precision and recall, and is an overall score to capture the innate tradeoff between the two. We tuned and scored our models with an eye toward maximizing this score. 


## Conclusion

> We did find several features that do contribute to a flight delay. Notably the departure time of day is particularly important, as is the segment number that the aircraft is flying for the day, which are certainly related.  And it makes sense that as the day goes on, aircraft are more likely to be delayed. Now it's important to note that although this chart implies a strong contribution from the departure block, it actually only accounts for 20 percent of the variance in flight delays. And all of these elements down here starting with Snowfall are accounting for less than 5 percent of that variance. This doesn't bode well for predictive quality.
>![Figure 1 - Delay Contributors](https://github.com/threnjen/flatiron_module_03_project/blob/main/images/delay_contributors.png)


> Let's take a quick look at Departure Block. This chart is organized from low to high delay per block and although it's not in order of time you can see along that the bottom that it pretty generally follows time of day. This second block here is a large overnight block that ends just before morning and is technically part of the early morning, and you can see as delays increase that the time is generally getting later. There is a pretty clear relationship here, which is why this shows up as the most strongly correlated predictor.
>![Figure 2 - Departure Block Delay](https://github.com/threnjen/flatiron_module_03_project/blob/main/images/departure_block.png)

#### Can we anticipate a delay with the Bureau's current collection metrics?

> Despite a robust and varied group of potential delay contributors, and even individual elements that clearly do contribute to delays when they happen, we could not form a model that reliably anticipates delay First, we predicted FAR more delays than were actually true. Only 20.3% of the delays we predicted were delays. Next we predicted just over half of the ACTUAL delays at 58.6%. And finally, our model's overall skill at distinguishing classes was poor. A model with a 50% AUC has no distinguishing skill and ours had only 60.7%. These are very poor results.
>![Figure 3 - Scores](https://github.com/threnjen/flatiron_module_03_project/blob/main/images/scores.png)
>![Figure 4 - Confusion Matrix](https://github.com/threnjen/flatiron_module_03_project/blob/main/images/confusion_matrix.png)

#### Given a delay, can we predict why the delay occurred?
> WHY can't we find the delays? For this we go a step deeper into reasons for delay, which is information that we do have, and we saw that our top reason for a delay is a Late Aircraft, meaning the tail number that a flight is preparing to leave on was late to arrive to the airport on its previous segment. This is very consistent with learning that the Departure Block and Segment Numbers are known correlators. But it also creates a kind of self-referential problem where, and this is really common sense, delays cause more delays. A flight comes in late and all subsequent flights that day will probably be late as well. And it turns out that this is really difficult to anticipate.
> ![Figure 5 - Confusion Matrix](https://github.com/threnjen/flatiron_module_03_project/blob/main/images/delay_type.png)


> These weak predictions can actually be explicitly visualized and it will make sense why this isn't working. 
> The visual type below takes all of our different possible predictive elements and makes them into a kind of 2D map where data that is similar in characteristics are clumped together and then we can visually see how similar outcomes share similar characteristics. 

> ![Figure 6 - UMAP - strong set](https://github.com/threnjen/flatiron_module_03_project/blob/main/images/umap_example.png)

> Above we have an *unrelated sample problem* which is sorting products on a website into categories. In the sample problem you can see strong groupings of similar items.


>  ![Figure 7 - UMAP - our set](https://github.com/threnjen/flatiron_module_03_project/blob/main/images/umap_delays_500.png) 

> Above we have our map for specific delay type. We notice that in our problem, the entire map looks like a paint spatter. The delay problem has not been solved by us - even with all of our features there are not strong groupings of like-features that help conclusively determine any type of delay. It's no wonder, seeing this visual, that our model struggles to conclusively sort our flights.


#### With this information in hand - can the Bureau provide resources to help reduce delay?
> While innately we might want to think that weather and airport inefficiencies cause a lot of the delay, ultimately CARRIERS cause most of their own delay. That means that if they want to improve delays, they focus internally on improving their own operational inefficiencies, and there isn't much that the bureau can do to help. Simply, the area of carrier delay encapsulates company inefficiencies for which the Bureau of Transportation doesn't have the predictors. The Bureau cannot at this time offer any resources for delay reduction. Recommendations will be for airline-specific actions to improve delay metrics.
>The largest visible contributors that we do have revolve around departure block and segment number, so minor recommendations can be made on that.



## Recommendations for Future Work

> Airlines should embark on an internal study of service methods and metrics in order to increase their operating efficiencies, which should result in the greatest overall improvement to delay, since Carrier Delay is the largest delay type

> A feasibility study on improving the airline’s nationwide flight map to see if overall segments can be reduced and departure blocks shifted to less busy times of day. These small alterations, in conjunction with a review of internal carrier services, may be enough to offer some improvement to delay.



## Presentation
[Video - Data Science Module 3 Project](https://youtu.be/pITRcrt9wXk)

[PDF of Presentation](https://github.com/threnjen/flatiron_module_03_project/blob/main/DSC_Mod_3.pdf)





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
