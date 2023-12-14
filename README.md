# Recipes_Prediction_Model

## Framing the Problem

### Problem Identification

We are trying to predict the number of calories a recipe may contain because we thought there may be discoverable correlations between that and its other nutritional content such as the protein, carbohydrates, fats, sugars, and etc. In the data cleaning phase, similar steps to previous projects were undertaken, with additional considerations specific to predicting recipe calories. The dataframe was narrowed down to relevant columns, focusing on variables directly related to nutritional content. The nutrition column was further utilized to derive new columns, such as protein, carbohydrates, and other nutritional labels. This feature engineering step was crucial in extracting specific information that could contribute to predicting the number of calories in a recipe.

- **Response Variable**: 
Our response variable is 'calories', which was picked because it is a continuous numerical variable that can accurately represent our predictions. Calories are a common unit for nutritional information, extremely important to overall health and wellness, and are essential macronutrients. Therefore predicting calories can enable a more nuanced understanding of energy intake, diet, and how individuals can try to take a more informed approach on dietary choices. 

- **Evaluation Metric**: 
The metric that we selected to evaluate the decision tree regression model is R-squared. This measures the proportion of variance from the dependent variable that can be predicted by the independent variables. In our prediction question, a higher R-squared value indicates a better model fit, which suggests there is a greater share of variability in the caloric content accounted for by selected features. 

- **Time of Prediction Information**: 
The information we are given at the time of prediction would be everything within the inital dataframe which includes the variables that we used for our baseline modeling. These initial variables used are `carbohydrates` and `protein`. These variables would be known at the time of prediction because when a recipe is submitted, these are information that accompany the submission so in order to predict the calories of the recipes, these information would be available.

**Below Visualization**

|     id | name                                 |   minutes |   n_steps |   n_ingredients |   total fat |   sugar |   sodium |   protein |   saturated fat |   carbohydrates |   calories |
|:-------|:-------------------------------------|:----------|:----------|:----------------|:------------|:--------|:---------|:----------|:----------------|:----------------|:-----------|
| 333281 | 1 brownies in the world    best ever |        40 |        10 |               9 |          10 |      50 |        3 |         3 |              19 |               6 |      138.4 |
| 453467 | 1 in canada chocolate chip cookies   |        45 |        12 |              11 |          46 |     211 |       22 |        13 |              51 |              26 |      595.1 |
| 306168 | 412 broccoli casserole               |        40 |         6 |               9 |          20 |       6 |       32 |        22 |              36 |               3 |      194.8 |
| 286009 | millionaire pound cake               |       120 |         7 |               7 |          63 |     326 |       13 |        20 |             123 |              39 |      878.3 |
| 475785 | 2000 meatloaf                        |        90 |        17 |              13 |          30 |      12 |       12 |        29 |              48 |               2 |      267   |


**Data cleaning** 
The data cleaning we used was taken from our Project 3, but we decided to add more columns with data taken from the nutrition column because it assists us in our further modeling and training/testing sets. Columns such as `protein`, `carbohydrates`, `total fat`, `sugar`, `sodium`, and `saturated fat` were added for us to use in our baseline modeling. 


## Baseline Model

- **Description**: 
For our baseline model, we used the 'recipes' DataFrame to predict our target variable 'calories' with features such as `protein` and `carbohydrates`. We chose these features because they are both quantitative and continuous, and to keep it that way we decided to stray from any categorical transformations of our data. The features we chose also have a general correlation with calories. No ordinal or nominal features were used in our implementation. The model used a RandomForestRegressor within the pipeline which also includes a preprocessor step with StandardScalar for the features `carbohydrates` and `protein`. We split the data into two sets, training and testing, with 80% used for the training and 20% used for the testing. We fit our model on the training and generated scores. 

- **Model Performance**: 
Our model's performance is tested through the R-squared metric. We view our scores for the training and test set which provides insight into how well our model explains the variance in our target variable. The current model is not perfect as the r-squared metric returns a score of around of .8. Reasons behind this can be the features we chose or didn't choose as there may be better or more we can include that would lead to a higher score. The current modeling is an extremely naive approach that only predicts a single class, which may be an indicator of dataset imbalances such as oversampling/undersampling. Our model is currently limited in handling imbalances.

## Final Model

- **Features Added**:
Our final model includes two new features, `total fat` and `n_ingredients`, to our original features `protein` and `carbohydrates`. Reasoning behind choosing `total fat` is that in foods a higher fat content has impact on it's caloric content while the `n_ingredients` may possibly reflect a more complex dish which can influence caloric content. The addition of these features is to try and have a more well-rounded and comprehensive set of variables that may contribute to our overall prediction. 

- **Hyperparameters**:
Our chosen final model is a DecisionTreeRegressor, which works well with capturing non-linear relationships in data. The hyperparameters that we picked after thorough experimentation were 'max-depth' of `None` and a 'min_samples_split' of '2'. We tuned these parameters through an evaluation on the training and testing sets. We picked these hyperparamters while keeping in mind possible trade-offs in model complexity and overfitting. 

- **Final Model Performance**:
Our final model's performance is evaluated using r-squared metric. As we can see, the R-squared values show a substantial improvement over time from our baseline model, with a final R-squared value of .99 in comparison to the baseline model's R-squared value of .8xx. The significant increase in our R-squared values indicate that our final model is better fitted to the data and captures higher proportion of variance in our target `calories`. The superior perfomance of our final model is an indicator of the accuracy in predicting caloric content of the recipes. 

- **Visualization**:

<iframe src="assets/scatter_plot.html" width=800 height=600 frameBorder=0></iframe>