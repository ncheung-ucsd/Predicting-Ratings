# Predicting Ratings

### Problem Identification

The prediction problem for this project was to predict the average rating, rounded to the nearest rating that a recipe would recive. This is a classification problem, specifically a Multi-class classifcation since there are more than two classes that a data point could be classified to: one of five ratings from 1-5.

The response variable was the rounded average rating, and the data that was used to predict was: total fat (PDV), sugar (PDV), minutes, and review. We would have all this information during the time of prediction, because this model was built to be used to fill in missing average rounded ratings in a dataset similar to the one used above. Thus, all data would be available.

Accuracy was chosen over F1-score because precision was not any more or less important than recall, therefore the extra information gained by the F1-score was not important, since neither false positives nor false negatives are more important than the other. Accuracy was then chosen for its simplicity.

### Baseline Model

The baseline model was a Decision Tree, where default arguments from sklearn were used. Notably, this meant an uncotrolled max_depth and a min_samples_split of 2. The features that were used were: total fat (PDV) and sugar (PDV). These features are quantitative, and no transformations were done to these features.

The baseline model achieved a training accuracy of approximately 0.755, and a testing accuracy of 0.636. This is an indication that this is not a good model, because it only classified 63.6% of data points correctly, which is quite low. In addition, the training accuracy is higher than the testing accuracy, which indicates that the model does not generalize well to unseen data and is overfitted to the training set.

### Final Model

The features that were added were: minutes and review. Minutes was good for the data and prediction task because it was hypothesized that recipes that took longer were more likely to receive lower ratings, since users would grow impatient, therefore it would be helpful in prediction. Review was good for the data and prediction task because it was hypothesized that negative reviews would receive lower ratings, while positive reviews would recieve higher ratings. Thus it would be also useful as a feature in prediction.

Minutes, sugar (PDV), and total fat (PDV) were transformed with a QuantileTransformer, to limit the impact of outliers. The review column is a column of strings, and was transformed using the TF-IDF.

The model that was chosen was a Decision Tree with a controlled max_depth of 1 and a min_samples_split of 2. These hyperparameters were chosen using Grid Search, where max_depths of 1, 2, 3, 4 and 5 were tested, while min_sample_split of 2, 3, and 4 were tested.

The final model achieved a training accuracy of approximately 0.701, and a testing accuracy of approximately 0.702. This is an improvement over the baseline model because the testing accuracy is much higher (0.702 vs 0.636), which indicates that the final model better generalizes to unseen data. Also, the training accuracy and the testing accuracy do not have much of a disrepancy for the final model, which implies that the model is no longer overfitted to the training set.

### Fairness Analysis

The first step taken was to left merge the two datasets together. This was done to explore potential relationships between the number of calories in a recipe and the ratings those recipes received. The next step was to fill all ratings of 0 with `np.nan`. This was done because zeroes in the dataset indicated that the values were missing, not that the user gave the recipe a rating of 0, since the lowest possible rating a user can give is 1. Thus, `np.nan` is a better representation of the value. The next step was to add the average rating per recipe back to `RAW_recipes`. This was to aggregate each pair of recipe and rating of a given recipe into one row, so that each recipe only had one row. The next step was splitting the `nutrition` column into
One row for every recipe, merged has one row for every pair of recipe and rating for a recipe. This was done so that analysis can be done on the relationships between the number of calories and individual nutrients. The average ratings were also rounded, so that the rating could be represented as a categorical variable for each recipe, just as it appeared on the original `RAW_interactions.csv` dataset.

Below is the first few rows the dataframe. Note that the `tags`, `steps`, `description`, `ingredients`, `review` columns have been omitted because they were not used in the analysis and contained text that made the table format difficult to read.
