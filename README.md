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

| user_id | Identification of Recipe |
| recipe_id | Identification for the User |
| date | Date of an Interaction on The website |
| id | Recipe ID Number (identification)|
| rating | Rating Given by Reviewer |
| review | Actual Review Text given for recipe|










