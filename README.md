# Analysis on Recipe-Rating in Relation with Overall Calories

Author: Darren Ha

## Overview of Project:
This particular project was conducted in the DSC 80 at UCSD. It was meant to gauge the relationship between specific recipe's overall calories and their general rating. 

## Introduction:
The Dataset being observed within this project is a compilation of recipes gathered from food.com. The recipes themselves are organized by ID and were given a particular rating out of five which reflect individual user's experiences with the recipe. 

### Overarching Question:
## Does the Amount of calories within a specific recipe affect its Rating? ##

### The Data 
First Dataframe ('RAW_recipes.csv'):
The Raw Recipes Dataframe contains 83782 rows and 12 columns

### Column names and Descriptions to Note:

| Column Name | General Description |
| --- | --- |
| name | The Name of the particular recipe |
| id | Recipe ID Number (identification)|
| minutes | Duration needed to finish recipe |
| contributor_id | User ID or Identification of individual that submitted the Recipe|
| name | The Name of the particular recipe |
| submitted | Date that Recipe was submitted to website|
| tags | 'Tags' placed on Recipes to indicate favorable attributes|
| nutrition |nutrition information in list form: [Calories(PDV), Total fat(PDV), Sugar(PDV), Sodium(PDV), Protein(PDV), Saturated Fat(PDV), Carbohydrates (PDV)]|
| n_steps | Required amount of Steps to complete Recipe|
| steps | Numerical Steps to complete the Recipe (Instructions) |
| description | Description of The Recipe provide by the User |
| ingredients | List of individual Ingredients needed to make the Recipe|
| n_ingredients | Number of Ingredients required for the recipe |



Second Dataframe ('interactions.csv'):
The Interactions Dataframe contains 731927 rows and 5 columns

### Column names and Descriptions to Note:

| Column Name | General Description |
| --- | --- |
| user_id | Identification of Recipe |
| recipe_id | Identification for the User |
| date | Date of an Interaction on The website |
| id | Recipe ID Number (identification)|
| rating | Rating Given by Reviewer |
| review | Actual Review Text given for recipe|

## Why this Matters:

We will be looking at the information regarding calories in each row and seeing how it has an effect on peoples opinion on the recipe. Higher Calorie food is often associated with poor health and weight gain. It's often cited that good tasting food is usually higher in caloric value. Viewing this dataset can be an interesting lens on whether this common opinion is actually true.

## Data Cleaning and Exploratory Data:

### Step 1:
Began by merging the Two dataframes using the 'id' column of the Interactions Dataframe and the 'recipe_id' column of the Raw Recipes Dataframe.

### Step 2:
Following the merging of the Dataframes, all of the 0s within the Ratings Column would be replaced by np.nan. This is done because ratings on the website are only and usually between the rankings of 1 and 5. Therefore, ratings of zero within the dataframe indicate an individual not actually placing in a rating for their review. Therefore, these ratings must be replaced by 0 to not only prevent biases but also prepare the row for the Data cleaning being done in the next step.

### Step 3:
The Data cleaning within this instance also included the creation of an Average Ratings column within the Dataframe. To do this, first a series was created by grouping all of the ids together and getting a mean of all the ratings of recipes that shared the id. The Series was then merged with the main dataframe to create a new column, called 'rating_average'. This would now be the most applicable column for the future predictions regarding the overarching Question. 

### Step 4: 
Furthermore, due to the overarching question being the Average ratings in relation to total calories. There had to be a way to isolate the total amount of calories for each recipe. In this case, I created a new column called 'totalCalories' and assigned it to the first element in the list for nutrition, which are the calories for a specific recipe. From there the amount of calories for each particular recipe was easier to interpret.

Following Data Cleaning:
The new Dataframe contained 234429 rows and 19 columns

New Columns:
| Column Name | General Description |
| --- | --- |
| rating_average | Average Rating of a particular recipe |
| totalCalories | Number of Calories for particular recipe (Isolated from the Nutriton column) |


## Univariate Analysis:
For the Univariate Analysis the graph was made to observe the amount of recipes that got a particular average rating. Interestingly an enormous amount of the recipes within this dataset have very high ratings with an enormous amount of them having ratings of five.

<iframe src="avg_rating_distribution.html" width="800" height="600" frameborder="0"></iframe>

## Bivariate Analysis:
For the Bivariate Analysis, This particular plot is a Scatter Plot detailing the Average Rating of recipes in relation to their calorie count. Interestingly, the higher rated recipes are clustered around places with lower calorie counts, which is opposite to what many would expect.

<iframe src="calories_vs_rating.html" width="800" height="600" frameborder="0"></iframe>

## Interesting Aggregates:
Within this particular section focus was brought to the mean ratings, the amount of recipes within each calorie group and the standard deviation of each rating for each of the calorie groups. 

| calorieGroup   |   ('mean', 'rating_average') |   ('count', 'rating_average') |   ('std', 'rating_average') |
|:---------------|-----------------------------:|------------------------------:|----------------------------:|
| Low            |                      4.68086 |                        175529 |                    0.494435 |
| Medium         |                      4.66612 |                         43582 |                    0.497521 |
| High           |                      4.65242 |                          8834 |                    0.532019 |
| Very High      |                      4.64948 |                          3526 |                    0.555699 |

Interestingly, there is an enormous amount of recipes in the low calorie group which could explain why the mean rating for low calorie recipes are so high. There is also the fact that the standard Deviations for each calorie group increases as the amount of calories becomes higher. This suggests that the ratings for the recipes become more and more varied as the calories increase in the recipes.

## Assessment of Missingness:

## NMAR Analysis:
The column within this dataframe that most likely is NMAR is The 'rating_average' column. This is due to the fact that it exists as the successor to the 'review' column which is most likely to be empty due to individuals that used the recipe to having no opinion or an indifferent one causing them to purposely not leave a review on the that specific recipe. However in this case The Not Missing A Random Analysis will be done on the 'rating_average' column because it's more applicable to the overarching question.

## Missingness Dependency:
In order to test whether the 'rating_average' column is not missing at random it will be tested with a permutation test agianst the columns 'minutes' and 'n_ingredients'

Minutes Against Rating Average

Null Hypothesis: The missingness of Average Ratings does not depend on the amount of minutes needed to make the Recipe.

Alternate Hypothesis: The missingness of ratings does depend on the amount of minutes needed to make the recipe.

Test Statistic: The difference in mean minutes between recipes where rating_average is missing vs when rating_average is not missing

Significance Level: 0.05

P-Value: 0.024

The P-Value in this case meaning that the missingness of the average_ratings is dependent on the amount of time the recipe takes. In this case the null hypothesis is rejected

<iframe src="missingness_minutes.html" width="800" height="600" frameborder="0"></iframe>



Null Hypothesis: The missingness of Average Ratings does not depend on the amount of ingredients needed to make the Recipe.

Alternate Hypothesis: The missingness of ratings does depend on the amount of minutes ingredients needed to make the recipe.

Test Statistic: For n_ingredients, the difference in mean n_ingredients between recipes where rating_average is missing vs when rating_average is not missing

Significance Level: 0.05

P-Value: = 1

The P-Value in this case meaning that the missingness of the average_ratings is not dependent on the amount of time the recipe takes. In this case we fail to reject the null hypothesis. The Rating Average missingness is not dependent on the number of ingredients.


<iframe src="missingness_ingredients.html" width="800" height="600" frameborder="0"></iframe>

## Hypothesis Testing:

Circling back to the Overarching Question on whether or not the Amount of total calories affects the Average Rating of a Recipe. In this case we decided to do a permutation test to see if this is true.


**Null Hypothesis**: There is no difference of average rating between recipes with lower calorie count and higher calorie count.

**Alternate Hypothesis**: There is a difference of average rating between recipes with lower calorie count and higher calorie count

**Test Statistic**: Test Statistic will be difference in Means. 

Significance Level: 0.05

A Permutation test in this case was chosen because there was meant to be focus on whether the means of ratings between higher calorie or lower calorie were different. In order to begin this permutation test. I first had to split the recipes into two categories being high and low calorie classifications. This was done by finding the median of the calorie counts across the entire dataframe and then splitting all the recipes from there those having a lower than the median calorie count would be considered low calorie recipes and the high calorie recipes would be recipes that fall past the median. 

The **Observed Statistic** in this case was -0.017996080860049446.

After executing the Permutation Test it was shown that the resulting **P-Value** was very tiny being 0.0.

Due to this being significantly smaller than the Significance level. The Null Hypothesis is rejected in this case. It seems that there is a noticable difference in the average ratings between high and low calorie recipes. A potential reasoning for this somewhat lines up with the plotly we saw in the Bivariate Analysis. An enormous amount of the high ratings were scattered around low ratings. A potential explanation could be that lower calorie recipes are often looked upon with higher public opinion by default, therefore a higher rating is given as a byproduct.

## Framing a Prediction Problem

For the prediction Problem. I think it's best to focus on **Predicting the rating_average** of a particular recipe. The Type of problem would be **Regression** this is due to the fact that the elements in rating_average are often float numbers. The Response Variable in this case is also 'rating_average' which is the elements that we are trying to predict. This was chosen seeing as it connects to the earlier overarching question and there is also the fact that the information in the other columns most likely are very indicative of how the rating of the recipe will be. 

Model Evaluation will be measured using RMSE or Root Mean Squared Error. This would be a prudent perfromance gauger vecuase it is often possessing of the same units as the target variable which is rating points (1-5). It also prvents large errors from happening often because it penalizes them more harshley than small ones. 

Information that we know at the time of prediction that would be relevant would be the columns:
**totalCalories**, **n_ingredients**, **minutes**, and **n-steps**. These are already known and have good potential in helping us predict what we need.

Columns suh as **rating_average** and **review** are not good as features seeing as these columns are not known until an individual actually uses the recipe. 


## Baseline Model

The first baseline model will be a linear regression model. The features included would be the total calories (Column Name: totalCalories) which is quantitative. 
The number of ingredients (Column Name: n_ingredients) which is also quantitative. 
The model would predict the average rating of recipes(Column Name: rating_average). 

Initial RMSE was 0.4929900164996211. 

I believe that that initial RMSE is fair but it could be better. By my understanding a RMSE is shown to perform well if the number is as close to 0 as possible. 0.49 as an RMSE is barely closer to 0 than 1 therefore there could be some tweaks that could improve upon the model. 


## Final Model

One of the plans to improve this model is to add more features to it. To predict the average rating more accurately, adding columns to it such as the number of steps (Column Name: n_steps), and the time it takes to cook (Column Name: minutes) would potentially increase the performance of the model. These auxillary columns give the model more to work off of. 

Another plan of attack besides the features would be to put more 'imports' into the model. RandomForestRegressors to improve perfromance would be the first import. Another Import would be QuantileTransformer, this turns the columns into a more uniform distribution which is very useful for reducing the influence of outliers. The Column Transformer was also another thing that was added seeing as it editted columns such as 'totalCalories' and 'minutes' without affecting othe columns that were devoid of outliers. Lastly, GridSearchCV is used to improve the model as well seeing it selects the best hyperparameters to use in max_depth and n_estimators. 

The Best hyperparameters in terms of performance were model__max_depth = None and n_estimators = 100. 

The new Final Model had a **Root Mean Squared Error**: 0.3572747903917559

## Fairness Analysis

In order to do the Fairness Analysis I thought that it would be fitting to once again choose two groups of recipes that had to do with the overarching question. The Groups therefore were split into two groups of lower and Higher calories. 

Group X Chosen: High Calorie Count Recipes (Recipes with Total Calories >= median of 301.1)

Group Y Chosen: Low Calorie Count Recipes (Recipes with Total Calories < median of 301.1)

Evaluation Meric Utilized: Once Again will be RMSE, This would once again fit nicely because it measures prediction error in a simple way

Null Hypothesis: The Model used is fair for recipes in both Group X and Y. The RMSE found for higher calorie count recipes are about the same as lower calorie count recipes. Random Chance causes any noticable difference in RMSE.

Alternate Hypothesis: The Model used is not fair. The RMSE differs between recipes from Group X and Group Y. Difference in RMSE are not by random chance

Test Statistic: The difference between the RMSE of Group X and Group Y (High and Low Calorie Groups)

Significnace Level: 0.05


**Observed Root Mean Squared Error Difference**: 0.006862003872266542

**P-value**: 0.487

Conclusion After Tests: Due to the P-value being 0.487 being larger than the significance level of 0.05, the null hypothesis is failed to be rejected. The mdoel in this case seems to work well. There is little observed difference in the RMSE and therefore the final model seems to perform decently well for recipes in both Groups X and Y. Any of the Observed Differences are mostly likely spawning from random chance. 



































