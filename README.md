# Recipes Throughout Years
Exploratory Data Analysis and Visualizations
<br>

## Introduction

In this project we will be analyzing the ‘Recipes’ data set. This dataset details different recipes, their nutritional breakdown, the steps needed to complete them, and the user ratings. We were curious as to whether the recipes in the later years had the same rating distribution as the recipes in the earlier years.

Specifically the question we posed was: Do the recipes from the year 2018 have the same rating distribution as the recipes from earlier years?

We wanted to know whether the sheer abundance of existing recipes affects how the users rate the recipes. We hypothesize that the more recipes there are, the less likely they are to be very unique. We were curious if that or any other factors had an affect on the ratings. We care because this information can help recipe websites grow and expand faster as a business. The higher ratings the website has the more prestigious and reliable it is. If there was something that made the ratings different in the later year compared to earlier years, we would be able to work on another project to further investigate what caused the changes in the ratings.
<br>
Our dataset contains 234429 rows
<br>
<br>
The columns we are interested in are detailed below
<br><br>
| Columns      | Description |
| ----------- | :----------- |
| id      | Recipe ID       |
| minutes   | Time taken to prepare the recipe        |
| contributor_id   | ID of the user who submitted the recipe        |
| submitted   | The date when the user posted the recipe        |
| nutrition   | Nutrition information in the format of [calories (#), total fat (PDV),sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates(PDV)]|
| rating   | The rating of the recipe        |
| review   | The review left with the rating        |
| rating_avg   | The average rating for a specific recipe        |
| calories   | The number of calories in the recipe       |
| year   | The year in which the recipe was submitted        |

## Cleaning and EDA
When conducting our data cleaning process we cleaned several columns. 

#### Rating:
<br><br>
	We cleaned the rating column by replacing the “0” values with np.NaN values. This changed the amount of actual data that we have and can use. In fact, while conducting our permutation tests we chose to drop the rows with np.NaN values. We made this decision because while shuffling the years column and counting up every type of rating we noticed that the results were inconsistent. This is because the amount of np.NaN value within each year was different after every permutation, making it difficult to compare our data. 

#### Rating_avg:
<br><br>
	We also performed imputation of the ratings on the missing values. For every recipe we computed the average rating, and if any of the ratings were missing for that recipe we replaced it with that value. To make the data more readable and easier to manipulate we used pd.cut to transform float ratings into strict [1, 2, 3, 4, 5] rating by rounding down.
	
#### Submitted:
<br><br>
	We changed the submitted column to only contain the year the recipe was submitted in, to better suit our graphs and analysis. Since we are only interested in the year that the rating was submitted in, we changed that column to match.

#### Calories:
<br><br>
	The nutrition column had several different nutrition labels. We were interested in trends between calories and ratings, so we decided to extract the caloric value of each recipe from the nutrition column and add it as a new column.

<iframe src="assets/calories-and-year.html" width=800 height=600 frameBorder=0></iframe>
