# Analysis on Recipe Rating in Relation with Overall Calories

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

## Step 1:
Began by merging the Two dataframes using th 'id' column of the Interactions Dataframe and the 'recipe_id' column of the Raw Recipes Dataframe.

## Step 2:
Following the merging of the Dataframes, all of the 0s within the Ratings Column would be replaced by np.nan. This is done because ratings on the website are only and usually between the rankings of 1 and 5. Therefore, ratings of zero within the dataframe indicate an individual not actually placing in a rating for their review. Therefore, these ratings must be replaced by 0 to not only prevent biases but also prepare the row for the Data cleaning being done in the next step.

## Step 3:
The Data cleaning within this instance also included the creation of an Average Ratings column within the Dataframe. To do this, first a series was created by grouping all of the ids together and getting a mean of all the ratings of recipes that shared the id. The Series was then merged with the main dataframe to create a new column, called 'rating_average'. This would now be the most applicable column for the future predictions regarding the overarching Question. 

## Step 4: 
Furthermore, due to the overarching question being the Average ratings in relation to total calories. There had to be a way to isolate the total amount of calories for each recipe. In this case, I created a new column called 'totalCalories' and assigned it to the first element in the list for nutrition, which are the calories for a specific recipe. From there the amount of calories for each particular recipe was easier to interpret.

Following Data Cleaning:
The new Dataframe contained 234429 rows and 19 columns

New Columns:
| Column Name | General Description |
| --- | --- |
| rating_average | Average Rating of a particular recipe |
| totalCalories | Number of Calories for particular recipe (Isolated from the Nutriton column) |

















