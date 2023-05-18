# Recipes Throughout Years
Exploratory Data Analysis and Visualizations
<br>

## Introduction

In this project we will be analyzing the ‘Recipes’ data set. This dataset details different recipes, their nutritional breakdown, the steps needed to complete them, and the user ratings. We were curious as to whether the recipes in the later years had the same rating distribution as the recipes in the earlier years.

Specifically the question we posed was: Do the recipes from the year 2018 have the same rating distribution as the recipes from earlier years?

We wanted to know whether the sheer abundance of existing recipes affects how the users rate the recipes. We hypothesize that the more recipes there are, the less likely they are to be very unique. We were curious if that or any other factors had an affect on the ratings. We care because this information can help recipe websites grow and expand faster as a business. The higher ratings the website has the more prestigious and reliable it is. If there was something that made the ratings different in the later year compared to earlier years, we would be able to work on another project to further investigate what caused the changes in the ratings.
<br><br>
Our dataset contains 234429 rows
<br><br>
The columns we are interested in are detailed below
<br><br>
| Columns            | Description  |
| ------------------ | :----------- |
| id                 | Recipe ID       |
| minutes            | Time taken to prepare the recipe |
| contributor_id     | ID of the user who submitted the recipe |
| submitted          | The date when the user posted the recipe |
| nutrition          | Nutrition information including calories (#), total fat (PDV),sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates(PDV) |
| rating             | The rating of the recipe |
| review             | The review left with the rating |
| rating_avg         | The average rating for a specific recipe |
| calories           | The number of calories in the recipe |
| year               | The year in which the recipe was submitted |

## Cleaning and EDA
When conducting our data cleaning process we cleaned several columns. 

#### Rating:
We cleaned the rating column by replacing the “0” values with np.NaN values. This changed the amount of actual data that we have and can use. In fact, while conducting our permutation tests we chose to drop the rows with np.NaN values. We made this decision because while shuffling the years column and counting up every type of rating we noticed that the results were inconsistent. This is because the amount of np.NaN value within each year was different after every permutation, making it difficult to compare our data. 

#### Rating_avg:
We also performed imputation of the ratings on the missing values. For every recipe we computed the average rating, and if any of the ratings were missing for that recipe we replaced it with that value. To make the data more readable and easier to manipulate we used pd.cut to transform float ratings into strict [1, 2, 3, 4, 5] rating by rounding down.
	
#### Submitted:
We changed the submitted column to only contain the year the recipe was submitted in, to better suit our graphs and analysis. Since we are only interested in the year that the rating was submitted in, we changed that column to match.

#### Calories:
The nutrition column had several different nutrition labels. We were interested in trends between calories and ratings, so we decided to extract the caloric value of each recipe from the nutrition column and add it as a new column.
#### Our Cleaned DataFrame
|     id |   minutes |   contributor_id | submitted   | nutrition                                    |   rating | review                                                                                                                                                                                                                                                                                                                                           |   rating_avg |   calories |   year |
|-------:|----------:|-----------------:|:------------|:---------------------------------------------|---------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------:|-----------:|-------:|
| 333281 |        40 |           985201 | 2008-10-27  | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]     |        4 | These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.                                                                                   |            4 |      138.4 |   2008 |
| 453467 |        45 |          1848091 | 2011-04-11  | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0] |        5 | Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, & I made the whole batch & used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe! |            5 |      595.1 |   2011 |
| 306168 |        40 |            50969 | 2008-05-30  | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |        5 | This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!                                                                                                                                  |            5 |      194.8 |   2008 |
|        |           |                  |             |                                              |          | The photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.                                                                                                                                                                                                        |              |            |        |
|        |           |                  |             |                                              |          | Thanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family's favorite Zaar cookbook :)                                                                                                                                                                                                                          |              |            |        |
| 306168 |        40 |            50969 | 2008-05-30  | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |        5 | I made this for my son's first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.                                                                                                                                                                               |            5 |      194.8 |   2008 |
| 306168 |        40 |            50969 | 2008-05-30  | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |        5 | Loved this.  Be sure to completely thaw the broccoli.  I didn&#039;t and it didn&#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.                                                                                                                                                     |            5 |      194.8 |   2008 |


### Univariate Data
<iframe src="assets/dist-avg-ratings.html" width=800 height=600 frameBorder=0></iframe>
We created a density histogram that describes the proportion of each rating. As you can see on the graph it seems like a left skewed distribution. Thus, the majority of ratings fall into the 4 or 5 star category, while the rest of the ratings are 1, 2, or 3 stars. It seems that people tend to leave higher ratings rather than lower ratings for the recipes. People probably feel more strongly about the things that they liked and want to share with the world, rather than the things that they didn’t like or thought were just ok. 

### Bivariate Data
<iframe src="assets/year-and-ratings.html" width=800 height=600 frameBorder=0></iframe>
We made a scatterplot with years on the x-axis and average rating on the y-axis. As you can see on the graph, there tends to be more points towards the higher ratings in general. There also seems to be more points in earlier years. For example, in 2008, the points from 3-5 form a line showing that the majority of points are in that region. In contrast, in 2018, there are a lot of points around 4-5 rating and there are more gaps in the data. This shows that while the trend of having more points towards higher ratings is consistent, there is less data in 2018.

### Aggregate Data

This is a table grouped by year, that takes the mean of the rating column for every year. The mean values tend to range between 4.46 and 4.71. We wanted to know if such differences were significant or not.

|   rating |
|---------:|
|  4.66142 |
|  4.68105 |
|  4.69894 |
|  4.70747 |
|  4.72201 |
|  4.70401 |
|  4.71736 |
|  4.68498 |
|  4.50763 |
|  4.46356 |
|  4.49537 |