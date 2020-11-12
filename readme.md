# Predicting Food Deserts

Jose Ramirez

## Social Case

The United States of America leads the world in both obesity and diabetes rates. Many Americans struggle with these conditions as a result of not having access to healthy food.

If the federal government had access to a model that could predict whether a census tract was likely to be a food desert or not based off of socioeconomic features, they could then provide assistance to areas that need it most.
This would be an important model because the USDA only releases a list of food deserts every 5 years. However, the United States Census Bureau releases yearly census estimates. This new information could be used to update the model each year and identify areas likely to become food deserts that were not previously.

## Repository Structure
* pngs -- folder that contains visualizations that were vital to my analysis
* 01_DataCleaning -- preprocessing data
* 02_EDA_FeatureEngineering -- exploratory data analysis and feature engineering
* 03_Modeling -- contains the different models run on the dataset
* 04_PostModelingAnalysis -- contains analysis of modeling results
* README.md
* presentation.pdf -- contains pdf version of project presentation

## Data

For this project, data from the Economic Research Service of the USDA was utlized. This dataset has over 72,865 rows and 147 features. This was then combined with both demographical and educational attainment datasets from the United States Census Bureau. After performing preprocessing, statistical tests, and feature engineering, 51 features were used for modeling, including engineered features.

## Statistical Tests and Feature Engineering

After preliminary exploratory data analysis, there were hypotheses that needed to be tested:

* Does living in an urban environment make it more likely that a person lives in a food desert?

	<img src="https://raw.githubusercontent.com/Sonora27/food_desert_classification/master/pngs/Type%20of%20Census%20Tract.png">

	* From the proportion test with a test statistic of 61.99 and a p-value of 0, the null hypothesis that the proportions are equal for people that live in an urban environment and people who live in a rural environment can be rejected. As a result, this has been identified as an important feature and will be kept for modeling.

* Does having low access to a vehicle and living in an urban environment make it more likely to live in a food desert than living in an urban environment alone?

	<img src="https://raw.githubusercontent.com/Sonora27/food_desert_classification/master/pngs/FDR%20by%20VA%20in%20Urban%20Environment.png">

	* From the proportion test with a test statistic of 27.24 and a p-value of 2.28x10^-163, the null hypothesis that the proportions are equal for people with low vehicle access that live in an urban environment and people who live in an urban environment alone can be rejected. As a result, this engineered feature has been identified as important and will be kept for modeling.


## Modeling

For model evaluation, recall was used as the primary evaluation metric. This is so that false negatives can be reduced as much as possible. In this case, a False Negative would be saying a Census Tract is not a food desert when it in fact is. As it pertains to this particular social case, it would be most detrimental for the final model to have a false negative because it would mean the government would miss areas likely to become food deserts.

In addition, F1 was used as a secondary evaluation metric to achieve somewhat of a balance between false negatives and false positives. Although not the priority, the model should try not to cause the government to waste precious resources on areas that are not food deserts.

To deal with class imbalance, TomekLinks was used. Undersampling was a good choice in this instance because there was enough data in both classes and as a result, there was no fear of data loss.

### Decision Tree

The Decision Tree model ended up with a recall score of .75 and an F1 score of .68.

### Random Forest

The Random Forest model ended up with a recall score of .77 and an F1 score of .70.

### XG BOOST

For my XG Boost model, I used a combination sampling technique called SMOTEENN. This technique uses SMOTE to oversample the minority class, but then it uses a K Nearest Neighbots of 3 to undersample the majority class. This helps prevent the overfitting that usually accompanies the SMOTE technique.

Using XG BOOST with SMOTEENN, a recall of .79 was achieved as well as an F1 Score of .67. This was used as the final model for analysis.

## Conclusions

	<img src="https://raw.githubusercontent.com/Sonora27/food_desert_classification/master/pngs/FDR%20by%20VA%20in%20Urban%20Environment.png">




Sources: 

https://health.usnews.com/health-news/health-wellness/articles/2014/05/28/america-tops-list-of-10-most-obese-countries

https://endocrinenews.endocrine.org/u-s-leads-developed-nations-in-diabetes-prevalence/