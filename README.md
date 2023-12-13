# Recipes_Prediction_Model

## Framing the Problem

### Problem Identification

We are trying to predict the number of calories a recipe may contain because we thought there may be discoverable correlations between that and its other nutritional content such as the protein, carbohydrates, fats, sugars, and etc. In the data cleaning phase, similar steps to previous projects were undertaken, with additional considerations specific to predicting recipe calories. The dataframe was narrowed down to relevant columns, focusing on variables directly related to nutritional content. The nutrition column was further utilized to derive new columns, such as protein, carbohydrates, and other nutritional labels. This feature engineering step was crucial in extracting specific information that could contribute to predicting the number of calories in a recipe.

- **Response Variable**: Our response variable is 'calories', which was picked because it is a continuous numerical variable that can accurately represent our predictions. Calories are a common unit for nutritional information, extremely important to overall health and wellness, and are essential macronutrients. Therefore predicting calories can enable a more nuanced understanding of energy intake, diet, and how individuals can try to take a more informed approach on dietary choices. 

- **Evaluation Metric**: The metric that we selected to evaluate the decision tree regression model is R-squared. This measures the proportion of variance from the dependent variable that can be predicted by the independent variables. In our prediction question, a higher R-squared value indicates a better model fit, which suggests there is a greater share of variability in the caloric content accounted for by selected features. 

- **Time of Prediction Information**: The information we are given at the time of prediction would be everything within the inital dataframe which includes the variables that we used for our baseline modeling. These initial variables used are `carbohydrates` and `protein`.

***insert data cleaning here

## Baseline Model







