# Recipes_Prediction_Model

## Framing the Problem

### Problem Identification

We aim to predict the caloric content of a recipe because there seems to be discoverable correlations between number of calories and its other nutritional content such as the protein, carbohydrates, fats, sugars, and etc. The selection of regression models is motivated by the continuous nature of the target variable, calories. Regression analysis proves ideal when the objective is to predict a continuous quantity, allowing us to establish a nuanced understanding of a recipe's energy content.

- **Data Cleaning**:

|     id | name                                 |   minutes |   n_steps |   n_ingredients |   total fat |   sugar |   sodium |   protein |   saturated fat |   carbohydrates |   calories |
|:-------|:-------------------------------------|:----------|:----------|:----------------|:------------|:--------|:---------|:----------|:----------------|:----------------|:-----------|
| 333281 | 1 brownies in the world    best ever |        40 |        10 |               9 |          10 |      50 |        3 |         3 |              19 |               6 |      138.4 |
| 453467 | 1 in canada chocolate chip cookies   |        45 |        12 |              11 |          46 |     211 |       22 |        13 |              51 |              26 |      595.1 |
| 306168 | 412 broccoli casserole               |        40 |         6 |               9 |          20 |       6 |       32 |        22 |              36 |               3 |      194.8 |
| 286009 | millionaire pound cake               |       120 |         7 |               7 |          63 |     326 |       13 |        20 |             123 |              39 |      878.3 |
| 475785 | 2000 meatloaf                        |        90 |        17 |              13 |          30 |      12 |       12 |        29 |              48 |               2 |      267   |

The data cleaning we used was taken from our Project 3, but we decided to add more columns with data taken from the nutrition column because it assists us in our further modeling and training/testing sets. Columns such as `protein`, `carbohydrates`, `total fat`, `sugar`, `sodium`, and `saturated fat` were added for us to use in our modeling, specifically catering to our goal of predicting recipe calories as we felt these columns were directly correlated with number of calories.

- **Response Variable**: 
Our response variable is 'calories', which was picked because it is a continuous numerical variable that can accurately represent our predictions. Calories are a common unit for nutritional information, extremely important to overall health and wellness, and are essential macronutrients. Therefore predicting calories can enable a more nuanced understanding of energy intake, diet, and how individuals can try to take a more informed approach on dietary choices. 

- **Evaluation Metric**: 
The metric that we selected to evaluate our regression model is R-squared. This measures the proportion of variance from the dependent variable that can be predicted by the independent variables. In our prediction question, a higher R-squared value indicates a better model fit, which suggests there is a greater share of variability in the caloric content accounted for by selected features. 

- **Time of Prediction Information**: 
The information we are given at the time of prediction would be everything within the inital dataframe which includes the variables that we used for our baseline modeling. These initial variables used are `carbohydrates` and `protein`. These variables would be known at the time of prediction because when a recipe is submitted, these are information that accompany the submission so in order to predict the calories of the recipes, these information would be available.


## Baseline Model

- **Description**: 
For our baseline model, we used the 'recipes' DataFrame to predict our target variable 'calories' with features such as `protein` and `carbohydrates`. We chose these features because they are both quantitative and continuous, and to keep it that way we decided to stray from any categorical transformations of our data. The features we chose also have a general correlation with calories. From our prior knowledge, we know that protein and carbohydrates are two factors that contribute to the calories of a dish and thus, we decided these are two features that would allow for accurate predictions of caloric content. No ordinal or nominal features were used in our implementation. The model used a RandomForestRegressor within the pipeline which also includes a preprocessor step with StandardScalar for the features `carbohydrates` and `protein`, this ensures that the numerical features are on a similar scale in an aim for good model performance. We split the data into two sets, training and testing, with 80% used for the training and 20% used for the testing. We fit our model on the training and generated scores. 

- **Model Performance**: 
Our model's performance is tested through the R-squared metric. We view our scores for the training and test set which provides insight into how well our model explains the variance in our target variable. The current model is not perfect as the r-squared metric returns a training score of around of 0.89 and a testing score of 0.74. Reasons behind this can be the features we chose or didn't choose as there may be better or more we can include that would lead to a higher score. The two features of `carbohydrates` and `protein` may not capture all relevant aspects that influences caloric content, so in order to have higher R^2 scores, we may want to have more features in our model. The current modeling is an extremely naive approach that only predicts a single class, which may be an indicator of dataset imbalances such as oversampling/undersampling. Our model is currently limited in handling imbalances.

## Final Model

- **Features Added**:
Our final model includes two new features, `total fat` and `n_ingredients`, to our original features `protein` and `carbohydrates`. Reasoning behind choosing `total fat` is that a higher fat content has impact on it's caloric content while the `n_ingredients` may possibly reflect a more complex dish that is more caloric dense. The addition of these features is to try and have a more well-rounded and comprehensive set of variables that may contribute to our overall prediction. 

- **Hyperparameters**:
Our chosen final model is a Decision Tree Regressor, which works well with capturing non-linear relationships in data. The hyperparameters that we picked after thorough experimentation with `GridSearchCV` were 'max-depth' of 20 and a 'min_samples_split' of 2. We tuned these parameters through an evaluation on the training and testing sets. We picked these hyperparamters while keeping in mind possible trade-offs in model complexity and overfitting. These hyperparameters turned out to provide us with the highest R^2 scores.

- **Final Model Performance**:
Our final model's performance is evaluated using r-squared metric. As we can see, the R-squared values show a substantial improvement over time from our baseline model, with a final R-squared training score of .998 in comparison to the baseline model's R-squared training score of .892. In addition, the testing score improved from 0.747 to 0.971. The significant increase in our R-squared values as well as the increase in similarity between the training and testing score leads us to believe that the our final model is better fitted to the data. The improvement in the testing score indicates that our final model is able to predict calories of recipes well, not only on seen data, but also unseen data. 

| Model                                    |   Training Score |   Testing Score |
|:-----------------------------------------|:-----------------|:----------------|
| Final Model (Decision Tree)              |         0.998328 |        0.971128 |
| Baseline Model (Random Forest Regressor) |         0.891668 |        0.747383 |

- **Visualization**:

<iframe src="assets/scatter_plot.html" width=800 height=600 frameBorder=0></iframe>

This scatter plot helps visually showcase how well the final model's predictions align with the actual values.  Points that closely follow the diagonal line signify accurate predictions, showcasing the model's ability to estimate calories effectively. On the other hand, deviations from the diagonal line may indicate instances of prediction errors. The close proximity of the plotted points to the diagonal line suggests that the model generally makes accurate predictions regarding the calorie content of recipes based on the final model that we created.

- **Other Models Attempted**:
In our pursuit of the most effective predictive model, we experimented with different algorithms, including Linear Regression and Random Forest Regressor, to compare their R^2 scores. The Linear Regression model yielded R^2 scores around 0.5, indicating a moderate fit to the data. While the Random Forest Regressor demonstrated performance similar to our final Decision Tree Regressor, we opted against its use due to computational considerations. The Random Forest model not only required significantly more time to execute but also posed challenges during hyperparameter tuning using GridSearchCV, leading to kernel instability. We ultimately went with the Decision Tree Regressor as our final model because favorable balance between predictive accuracy and computational efficiency made it the most practical solution for our specific use case.

## Fairness Analysis
**Question**:
Is the model's performance affected by the number of ingredients in a recipe?

**Group X**: Recipes with a low number of ingredients (< 9).
**Group Y**: Recipes with a high number of ingredients (>= 9).

**Evaluation Metric**:
R-squared scores were used to assess the model's performance.

**Null Hypothesis**: Our model is fair. Its performance on recipes with low number of ingredients (quantified as less than 9 ingredients) is roughly the same as its performance on recipes with high number of ingredients.

**Alternative Hypothesis**: Our model is unfair. Its performance on recipes with low number of ingredients (quantified as less than 9 ingredients) is different than its performance on recipes with high number of ingredients.

**Test Statistic**:
The absolute difference in R-squared scores is the test statistic.

**Significance Level**:
We chose to use a significance level of 0.05.

**Conclusion**:
With a p-value of 0.914, we fail to reject the null hypothesis. This implies that the observed disparity in R^2 scores between recipes with low and high ingredient counts is likely attributable to random variability. In essence, there is insufficient evidence to substantiate the assertion that the model's performance significantly varies between these two groups. These results suggests that our model is indeed fair and does not vary according to number of ingredients. However, it's crucial to emphasize that this result doesn't lead us to an absolute conclusion. 
