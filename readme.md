# Predicting Food Deserts

Joe Ramirez

Data Sources: Sources: [USDA,](https://www.ers.usda.gov/data-products/food-access-research-atlas/download-the-data/) [CENSUS](https://data.census.gov/cedsci/)

## Social Case

The United States of America leads the world in both obesity and diabetes rates. Many Americans struggle with these conditions as a result of not having access to healthy food.

If the federal government had access to a model that could predict whether a census tract was likely to be a food desert or not based off of socioeconomic features, they could then use the [Healthy Food Financing Initiative](https://www.acf.hhs.gov/archive/ocs/programs/community-economic-development/healthy-food-financing) program to provide assistance to areas that need it most.

This would be an important model because the USDA only releases a list of food deserts every 5 years. However, the United States Census Bureau releases yearly census estimates. This new information could be used to update the model each year and identify areas likely to become food deserts that had not been previously identified.

## Repository Structure
* pngs -- folder that contains visualizations that were vital to my analysis
* 01_DataCleaning -- preprocessing data
* 02_EDA_FeatureEngineering -- exploratory data analysis and feature engineering
* 03_Modeling -- contains the different models run on the dataset as well as post modeling analysis
* README.md
* presentation.pdf -- contains pdf version of project presentation

## Data

For this project, data from the Economic Research Service of the USDA was utilized. This dataset has over 72,865 rows and 147 features. This was then combined with both demographical and educational attainment datasets from the United States Census Bureau. After performing preprocessing, statistical tests, and feature engineering, 51 features were used for modeling, including engineered features.

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

To deal with class imbalance, the combination sampling technique SMOTEENN was used. 

### Decision Tree

My Decision Tree model ended up with a recall score of .75 and an F1 score of .68.

### Random Forest

My Random Forest model ended up with a recall score of .77 and an F1 score of .70.

### XG BOOST

For the XG Boost model, a combination sampling technique called SMOTEENN was utilized. This technique uses SMOTE to oversample the minority class, but then it uses a K Nearest Neighbots of 3 to undersample the majority class. This helps prevent the overfitting that usually accompanies the SMOTE technique.

Using XG BOOST with SMOTEENN, a recall of .80 was achieved as well as an F1 Score of .67. This was used as the final model for analysis.

<img src="https://raw.githubusercontent.com/Sonora27/food_desert_classification/master/pngs/XGB_SMOTEENN_CM.png">

## Conclusions

<img src="https://raw.githubusercontent.com/Sonora27/food_desert_classification/master/pngs/feature_importance.png">

* From this graph it can be seen that the most important feature of the model was vehicle access. The United States federal government must improve vehicle access and public transportation in an effort to reduce the amount of food deserts in the country.
* In addition, the number of people in a census tract under the age of 18 was very important in our model. This suggest that companies may have a bias towards not building supermarkets in areas with a high amount of children as these may be seen as less profitable locations.

## Next Steps 

* Food swamps are areas where junk food stores and fast food restaurant outnumber supermarkets. It would be interesting to create a model that could predict food swamps and compare it to this food desert model.



### Sources: 

https://health.usnews.com/health-news/health-wellness/articles/2014/05/28/america-tops-list-of-10-most-obese-countries

https://endocrinenews.endocrine.org/u-s-leads-developed-nations-in-diabetes-prevalence/

https://ottawamagazine.com/eating-and-drinking/live-where-basics-are-missing-how-about-access-to-fresh-affordable-food-if-so-you-may-live-in-a-food-desert-even-downtown/

https://spoonuniversity.com/lifestyle/food-desert-obesity-rates

https://www.bluezones.com/2017/11/news-food-swamps-contribute-obesity-food-deserts/#:~:text=A%20food%20swamp%20is%20an,access%20to%20affordable%2C%20nutritious%20food.

https://today.uconn.edu/2017/11/food-swamps-predict-obesity-rates-better-food-deserts/