# Air Travel Delay Study (Module 3 Final Project)

For: Federal Bureau of Transportation

By: Jen Wadkins


## Introduction

> The Federal Bureau of Transportation has requested a report on if flight delay can be anticipated with their current collection metrics, with a goal of providing proper resources to individual carriers to assist in their reduction of delays.

## Questions

* Can we predict overall delay?
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
* Provide a "realtor simulator" model to compare with machine learning model
* Demonstrate ability of model to make new predictions
### Interpreting the Data
* Understand and describe the results

## Table of Contents


#### [OS_dataset_cleanup.ipynb](https://github.com/threnjen/flatiron_module_03_project/blob/master/OS_dataset_cleanup.ipynb

> * Project Overview
> * Obtaining our Data
> * Scrubbing/Cleaning our Data for OVERALL DELAY
> * Scrubbing/Cleaning our Data for SPECIFIC DELAY
> * Process Test Set


#### [EMN_modeling_Overall.ipynb](https://github.com/threnjen/flatiron_module_03_project/blob/master/EMN_modeling_Overall.ipynb

> * Project Overview
> * Exploring/Visualizing Data
> * Modeling
> * Model Evaluation
> * Conclusions and Recommendations
> * Future Work
> * Explanation of Attempts - Feature Engineering/Selection
> * APPENDIX

#### [EMN_modeling_Specific_Delay.ipynb](https://github.com/threnjen/flatiron_module_03_project/blob/master/EMN_modeling_Specific_Delay.ipynb

> * Project Overview
> * Exploring/Visualizing Data
> * Modeling
> * Model Evaluation


## Analysis

#### Q1?
> Answer 

#### Q2?
> Answer

#### Q3?
>Answer with picture example

>![Figure 1 - Housing Sales in King County by Location](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/comps_plat.png)

>more answer

#### Q4?

>Answer

> We did find several features that do contribute to a flight delay. Notably the departure time of day is particularly important, as is the segment number that the aircraft is flying for the day, which are certainly related.  And it makes sense that as the day goes on, aircraft are more likely to be delayed. Now it's important to note that although this chart implies a strong contribution from the departure block, it actually only accounts for 20 percent of the variance in flight delays. And all of these elements down here starting with Snowfall are accounting for less than 5 percent of that variance. This doesn't bode well for predictive quality.

> Let's take a quick look at Departure Block. This chart is organized from low to high delay per block and although it's not in order of time you can see along that the bottom that it pretty generally follows time of day. This second block here is a large overnight block that ends just before morning and is technically part of the early morning, and you can see as delays increase that the time is generally getting later. There is a pretty clear relationship here, which is why this shows up as the most strongly correlated predictor.

> Despite a robust and varied group of potential delay contributors, and even individual elements that clearly do contribute to delays when they happen, we could not form a model that reliably anticipates delay First, we predicted FAR more delays than were actually true. Only 20.3% of the delays we predicted were delays. Next we predicted just over half of the ACTUAL delays at 58.6%. And finally, our model's overall skill at distinguishing classes was poor. A model with a 50% AUC has no distinguishing skill and ours had only 60.7%. These are very poor results.

> WHY can't we find the delays? For this we go a step deeper into reasons for delay, which is information that we do have. And we see that our top reason for a delay is a Late Aircraft, meaning the tail number that a flight is preparing to leave on was late to arrive to the airport on its previous segment. This is very consistent with learning that the Departure Block and Segment Numbers are known correlators. But it also creates a kind of self-referential problem where, and this is really common sense, delays cause more delays. A flight comes in late and all subsequent flights that day will probably be late as well. And it turns out that this is really difficult to anticipate.

> These weak predictions can actually be explicitly visualized and it will make sense why this isn't working. 

## Conclusion

> And While innately we might want to think that weather and airport inefficiencies cause a lot of the delay, ultimately CARRIERS cause most of their own delay. That means that if we want to improve delays, they focus internally on improving their own operational inefficiencies, and there isn't much that the bureau can do to help there

> Simply, the area of carrier delay encapsulates company inefficiencies for which the Bureau of Transportation doesn't have the predictors







## Recommendations for Future Work

> Airlines should embark on an internal study of service methods and metrics in order to increase their operating efficiencies, which should result in the greatest overall improvement to delay, since Carrier Delay is the largest delay type
> A feasibility study on improving the airline’s nationwide flight map to see if overall segments can be reduced and departure blocks shifted to less busy times of day. These small alterations, in conjunction with a review of internal carrier services, may be enough to offer some improvement to delay.



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
