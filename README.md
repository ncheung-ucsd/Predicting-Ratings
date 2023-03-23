# Recipe and Interactions

### Problem Identification

This dataset includes recipes and ratings from the website [food.com](https://www.food.com). The question that the analysis will be centered around is: **What recipes tend to be lower in calories?**This question is important because understanding what types of recipes tend to be lower in calories can help individuals identify healthier food choices.

The original raw datasets include one for recipes, `RAW_interactions.csv`, and one for ratings, `RAW_ratings.csv`. `RAW_interactions.csv` has 83782 rows of data, and `RAW_interactions.csv` has 731927 rows of data. The relevant columns for this analysis are: `nutrition`, `n_steps`, `n_ingredients`, `rating`, and `review`. `nutrition` is the nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”. `n_steps` is the number of steps in the recipe. `n_ingredients` is the number of ingredients in the recipe. `rating` is the rating given. `review` is the review text.

### Baseline Model

The first step taken was to left merge the two datasets together. This was done to explore potential relationships between the number of calories in a recipe and the ratings those recipes received. The next step was to fill all ratings of 0 with `np.nan`. This was done because zeroes in the dataset indicated that the values were missing, not that the user gave the recipe a rating of 0, since the lowest possible rating a user can give is 1. Thus, `np.nan` is a better representation of the value. The next step was to add the average rating per recipe back to `RAW_recipes`. This was to aggregate each pair of recipe and rating of a given recipe into one row, so that each recipe only had one row. The next step was splitting the `nutrition` column into
One row for every recipe, merged has one row for every pair of recipe and rating for a recipe. This was done so that analysis can be done on the relationships between the number of calories and individual nutrients. The average ratings were also rounded, so that the rating could be represented as a categorical variable for each recipe, just as it appeared on the original `RAW_interactions.csv` dataset.

Below is the first few rows the dataframe. Note that the `tags`, `steps`, `description`, `ingredients`, `review` columns have been omitted because they were not used in the analysis and contained text that made the table format difficult to read.

### Final Model

The first step taken was to left merge the two datasets together. This was done to explore potential relationships between the number of calories in a recipe and the ratings those recipes received. The next step was to fill all ratings of 0 with `np.nan`. This was done because zeroes in the dataset indicated that the values were missing, not that the user gave the recipe a rating of 0, since the lowest possible rating a user can give is 1. Thus, `np.nan` is a better representation of the value. The next step was to add the average rating per recipe back to `RAW_recipes`. This was to aggregate each pair of recipe and rating of a given recipe into one row, so that each recipe only had one row. The next step was splitting the `nutrition` column into
One row for every recipe, merged has one row for every pair of recipe and rating for a recipe. This was done so that analysis can be done on the relationships between the number of calories and individual nutrients. The average ratings were also rounded, so that the rating could be represented as a categorical variable for each recipe, just as it appeared on the original `RAW_interactions.csv` dataset.

Below is the first few rows the dataframe. Note that the `tags`, `steps`, `description`, `ingredients`, `review` columns have been omitted because they were not used in the analysis and contained text that made the table format difficult to read.

### Fairness Analysis

The first step taken was to left merge the two datasets together. This was done to explore potential relationships between the number of calories in a recipe and the ratings those recipes received. The next step was to fill all ratings of 0 with `np.nan`. This was done because zeroes in the dataset indicated that the values were missing, not that the user gave the recipe a rating of 0, since the lowest possible rating a user can give is 1. Thus, `np.nan` is a better representation of the value. The next step was to add the average rating per recipe back to `RAW_recipes`. This was to aggregate each pair of recipe and rating of a given recipe into one row, so that each recipe only had one row. The next step was splitting the `nutrition` column into
One row for every recipe, merged has one row for every pair of recipe and rating for a recipe. This was done so that analysis can be done on the relationships between the number of calories and individual nutrients. The average ratings were also rounded, so that the rating could be represented as a categorical variable for each recipe, just as it appeared on the original `RAW_interactions.csv` dataset.

Below is the first few rows the dataframe. Note that the `tags`, `steps`, `description`, `ingredients`, `review` columns have been omitted because they were not used in the analysis and contained text that made the table format difficult to read.
