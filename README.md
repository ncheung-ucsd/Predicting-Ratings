# Predicting Ratings - Nathan Cheung

Our exploratory data analysis on this dataset can be found [here](https://ncheung-ucsd.github.io/RecipesEDA/).

### Problem Identification

The prediction problem for this project was to predict the average rating, rounded to the nearest rating that a recipe would recive. This is a classification problem, specifically a Multi-class classifcation since there are more than two classes that a data point could be classified to: one of five ratings from 1-5.

The response variable was the rounded average rating, and the data that was used to predict was: total fat (PDV), sugar (PDV), minutes, and review. We would have all this information during the time of prediction, because this model was built to be used to fill in missing average rounded ratings in a dataset similar to the one used. Thus, all data necessary would be available.

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

The first group was recipes where the minutes were less than or equal to 120. The second group was recipes where the minutes were greater than 100. The evaluation metric that was chosen was accuracy. Below are the null and alternative hypotheses

Null Hypothesis: Our model is fair. Its accuracy for recipes that take less than or equal to two hours and recipes that take more than an hour are roughly the same, and any differences are due to random chance.

Alternative Hypothesis: Our model is unfair. Its accuracy for recipes that take longer than two hours is lower than its accuracy for recipes that take less than or equal to two hours.

The test statistic that was used was difference in accuracy, and the significance value that was used was 0.05.

The permutation test generated a p-value of 0.0, which is below the cutoff of 0.05, thus we reject the null hypothesis that the model's accuracy for recipes that take less than or equal to two hours and recipes that take more than an hour are roughly the same, and any differences are due to random chance. This implies that the model is likely not fair.
