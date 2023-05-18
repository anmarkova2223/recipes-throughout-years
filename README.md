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
The columns we are interested in are detailed below
<br>
| Columns      | Description |
| ----------- | :----------- |
| id      | Recipe ID       |
| minutes   | Time taken to prepare the recipe        |
| contributor_id   | ID of the user who submitted the recipe        |
| submitted   | The date when the user posted the recipe        |
| nutrition   | Nutrition information in the format of [calories (#), total fat (PDV),sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]        |
| rating   | The rating of the recipe        |
| review   | The review left with the rating        |
| rating_avg   | The average rating for a specific recipe        |
| calories   | The number of calories in the recipe       |
| year   | The year in which the recipe was submitted        |
<iframe src="assets/calories-and-year.html" width=800 height=600 frameBorder=0></iframe>
