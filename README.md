# Recipes Throughout Years
Exploratory Data Analysis and Visualizations
Names: Anastasiya Markova and Yuhe Tian
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
| Column | Description |
| ----------- | ----------- |
| id | Recipe ID |
| minutes | Time taken to prepare the recipe |
| contributor_id | ID of the user who submitted the recipe |
| submitted | The date when the user posted the recipe |
| nutrition | Nutrition information including calories (#), total fat ,sugar, sodium, protein, saturated fat, carbohydrates |
| rating             | The rating of the recipe |
| review             | The review left with the rating |
| rating_avg         | The average rating for a specific recipe |
| calories           | The number of calories in the recipe |
| year               | The year in which the recipe was submitted |

## Cleaning and EDA
When conducting our data cleaning process we cleaned several columns. 

#### `rating`:
We cleaned the rating column by replacing the “0” values with np.NaN values. This changed the amount of actual data that we have and can use. In fact, while conducting our permutation tests we chose to drop the rows with np.NaN values. We made this decision because while shuffling the years column and counting up every type of rating we noticed that the results were inconsistent. This is because the amount of np.NaN value within each year was different after every permutation, making it difficult to compare our data. 

#### `rating_avg`:
We also performed imputation of the ratings on the missing values. For every recipe we computed the average rating, and if any of the ratings were missing for that recipe we replaced it with that value. To make the data more readable and easier to manipulate we used pd.cut to transform float ratings into strict [1, 2, 3, 4, 5] rating by rounding down.
	
#### `submitted`:
We changed the submitted column to only contain the year the recipe was submitted in, to better suit our graphs and analysis. Since we are only interested in the year that the rating was submitted in, we changed that column to match.

#### `calories`:
The nutrition column had several different nutrition labels. We were interested in trends between calories and ratings, so we decided to extract the caloric value of each recipe from the nutrition column and add it as a new column.
#### Our Cleaned DataFrame
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>id</th>
      <th>minutes</th>
      <th>contributor_id</th>
      <th>submitted</th>
      <th>nutrition</th>
      <th>rating</th>
      <th>review</th>
      <th>rating_avg</th>
      <th>calories</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>333281</td>
      <td>40</td>
      <td>985201</td>
      <td>2008-10-27</td>
      <td>[138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]</td>
      <td>4.0</td>
      <td>These were pretty good, but took forever to bake.  I would send it ...</td>
      <td>4.0</td>
      <td>138.4</td>
      <td>2008</td>
    </tr>
    <tr>
      <td>453467</td>
      <td>45</td>
      <td>1848091</td>
      <td>2011-04-11</td>
      <td>[595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0]</td>
      <td>5.0</td>
      <td>Originally I was gonna cut the recipe in half (just the 2 of us her...</td>
      <td>5.0</td>
      <td>595.1</td>
      <td>2011</td>
    </tr>
    <tr>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>[194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]</td>
      <td>5.0</td>
      <td>This was one of the best broccoli casseroles that I have ever made...</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>2008</td>
    </tr>
    <tr>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>[194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]</td>
      <td>5.0</td>
      <td>I made this for my son's first birthday party this weekend. Our gues...</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>2008</td>
    </tr>
    <tr>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>[194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]</td>
      <td>5.0</td>
      <td>Loved this.  Be sure to completely thaw the broccoli.  I didn&amp;...</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>2008</td>
    </tr>
  </tbody>
</table>


### Univariate Data
<iframe src="assets/dist-avg-ratings.html" width=800 height=600 frameBorder=0></iframe>
We created a density histogram that describes the proportion of each rating. As you can see on the graph it seems like a left skewed distribution. Thus, the majority of ratings fall into the 4 or 5 star category, while the rest of the ratings are 1, 2, or 3 stars. It seems that people tend to leave higher ratings rather than lower ratings for the recipes. People probably feel more strongly about the things that they liked and want to share with the world, rather than the things that they didn’t like or thought were just ok. 

### Bivariate Data
<iframe src="assets/year-and-ratings.html" width=800 height=600 frameBorder=0></iframe>
We made a scatterplot with years on the x-axis and average rating on the y-axis. As you can see on the graph, there tends to be more points towards the higher ratings in general. There also seems to be more points in earlier years. For example, in 2008, the points from 3-5 form a line showing that the majority of points are in that region. In contrast, in 2018, there are a lot of points around 4-5 rating and there are more gaps in the data. This shows that while the trend of having more points towards higher ratings is consistent, there is less data in 2018.

### Aggregate Data

This is a table grouped by year, that takes the mean of the rating column for every year. The mean values tend to range between 4.46 and 4.71. We wanted to know if such differences were significant or not.

|   year |   rating |
|-------:|---------:|
|   2008 |  4.66142 |
|   2009 |  4.68105 |
|   2010 |  4.69894 |
|   2011 |  4.70747 |
|   2012 |  4.72201 |
|   2013 |  4.70401 |
|   2014 |  4.71736 |
|   2015 |  4.68498 |
|   2016 |  4.50763 |
|   2017 |  4.46356 |
|   2018 |  4.49537 |

## Assessment of Missingness
In this dataset, we believe that the missingness type of missing values in `rating` would be NMAR. When we merge the `RAW_recipes.csv` and `RAW_interactions.csv`, we are doing a left outer merge which means that we would preserve the recipe even if there is no rating or comments made by users. Therefore, these recipes do not have ratings. The missing values in the `rating` column simply suggests that `rating` itself is missing.
In addition, we believe that users who really loved the recipes are more likely to rate the recipe. This also explains why `rating` would be NMAR since they are missing depending on how users liked it which is essentially the actual value itself.
<br>
<br>
As our question is centered around the distribution of rating in different years, our selected column would be `rating` and we are testing its missingness dependency on two columns: `calories` and `minutes`. In this case, we found our observed statistics to be the absolute difference in mean `calories` and `minutes` between the two groups of ratings missing and ratings not missing. We then run permutation tests 1,000 times to get 1,000 test statistics and calculate the probability of seeing values equal to or greater than our observed mean difference.
When testing whether `rating`’s missingness depends on `reviews`, our p-value is 0.0 which means the missingness of `rating` would potentially be dependent on the `reveiws` column.
When testing whether `rating`’s missingness depends on `minutes`, our p-value is 0.112 which means the missingness of `rating` would not be dependent on the `minutes` column.

## Hypothesis Testing

Our **null hypothesis** is that the distribution of ratings for recipes in 2018 is the same with the distribution of ratings for recipes for years before 2018. 
<br>
Our **alternative hypothesis** is that the distribution of ratings for recipes in 2018 is different from the distribution of recipes for years before 2018.
<br>
<br>
<iframe src="assets/hypothesis-test.html" width=800 height=600 frameBorder=0></iframe>
Our null hypothesis is that the distribution of ratings for recipes in 2018 is the same with the distribution of ratings for recipes for years before 2018. Our alternative hypothesis is that the distribution of ratings for recipes in 2018 is different from the distribution of recipes for years before 2018.
In this case, as we are examining the differences in categorical distributions, we are using the total variation distance between the two rating distributions in 2018 and years before 2018. Since the numbers of recipes posted in 2018 and years before 2018 are different, we are calculating the total variation distances using proportions in each rating category.
In our permutation test, we first drop the rows where ratings have NaN values as we would not want the number of missing rating values to differ in our two groups each time when we perform a permutation test.We then shuffle the `year` column and assign it as `shuffled_year`. We then group the data by 2018 and years before 2018 based on `shuffled_year`. After grouping the DataFrame into two groups, we get the proportions of the rating distribution for each of the groups and then take the total variation distance between the distributions. We would repeat the process 1,000 times to see what is the probability of seeing values equal to or even more extreme than our observed total variation distance.
Since we would like to fix our confidence interval at 0.05 and our p-value is 0.09, we would fail to reject the null hypothesis that the distribution of ratings for recipes in 2018 is the same with the distribution of ratings for recipes for years before 2018. 


