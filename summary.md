# Prediction Model for Student Performance

## Thought Process and Model Selection

In this project, I explored different base models to predict student performance based on various features such as gender, race/ethnicity, parental level of education, lunch type, and whether the student completed a test preparation course. The dataset provided consists of categorical features, which required careful handling before any model training.

### Initial Exploration (Rough Note)

My initial exploration involved testing several base models to evaluate which one performed best. The models tested included:

- Linear Regression
- Ridge Regression
- Lasso Regression
- Random Forest Regressor
- Gradient Boosting Regressor
- XGBoost
- LightGBM
- Support Vector Regression (SVR)
- KNN Regression
- CatBoost

Through experimentation, I found that the Stacking Regressor outperformed all other models. The stacking model, which combines multiple base models, proved to be more robust in capturing complex patterns in the data.

### Final Model (Predict Function)

After selecting the stacking model, I created a clean, structured notebook (called `predict`) that houses the final function to make predictions. Below is a summary of the model:

- **Base Learners:**

  - Linear Regression
  - Ridge Regression
  - Random Forest Regressor
  - Support Vector Regression

- Meta-model: Ridge Regression (used to combine the base learners)

The `predict_scores` function accepts a dataset as input, applies one-hot encoding for categorical features, trains the stacking model, and returns predictions for the input data.

The model was trained on a dataset, and predictions were generated for new or unseen data. This is useful for estimating the performance of students based on their characteristics.

```python
result = predict_scores(new_data)  # new_data is the DataFrame with input features

```

# Data Analysis

## ANOVA Results

I conducted an ANOVA (Analysis of Variance) to explore the relationship between categorical features and the target variable (`average_score`). Here are the results:

### ANOVA Results and Explanation:

#### Gender:

- **F-statistic**: 11.0692
- **p-value**: 0.0009
  **Explanation**: The p-value is less than 0.05, indicating a statistically significant difference in average scores between males and females. Gender does have an impact on student performance.

#### Race/Ethnicity:

- **F-statistic**: 6.2646
- **p-value**: 0.000059
  **Explanation**: The p-value is less than 0.05, indicating a statistically significant difference in average scores across different racial/ethnic groups. Race/ethnicity does have an impact on student performance.

#### Parental Level of Education:

- **F-statistic**: 6.4046
- **p-value**: 0.0000079
  **Explanation**: The p-value is less than 0.05, indicating a statistically significant difference in average scores based on the parents' education level. Parental level of education does impact student performance.

#### Lunch:

- **F-statistic**: 64.8270
- **p-value**: 0.0000000000000035
  **Explanation**: The p-value is significantly less than 0.05, indicating a very strong statistically significant difference in average scores based on lunch type. Students with standard lunch perform better than those with free/reduced lunch.

#### Test Preparation Course:

- **F-statistic**: 49.8818
- **p-value**: 0.0000000000039
  **Explanation**: The p-value is significantly less than 0.05, indicating a very strong statistically significant difference in average scores between students who completed the test preparation course and those who did not.

---

## Correlation with Average Score

The correlation between various features and the `average_score` is shown below:

| **Feature**                                    | **Correlation with Average Score** |
| ---------------------------------------------- | ---------------------------------- |
| gender_female                                  | 0.1249                             |
| gender_male                                    | -0.1249                            |
| race/ethnicity_group A                         | -0.0647                            |
| race/ethnicity_group B                         | -0.1101                            |
| race/ethnicity_group C                         | -0.0309                            |
| race/ethnicity_group D                         | 0.0514                             |
| race/ethnicity_group E                         | 0.1474                             |
| parental level of education_associate's degree | 0.0595                             |
| parental level of education_bachelor's degree  | 0.1175                             |
| parental level of education_high school        | -0.1656                            |
| parental level of education_master's degree    | 0.0571                             |
| parental level of education_some college       | 0.0324                             |
| parental level of education_some high school   | -0.0641                            |
| lunch_free/reduced                             | -0.2915                            |
| lunch_standard                                 | 0.2915                             |
| test preparation course_completed              | 0.2583                             |
| test preparation course_none                   | -0.2583                            |

---

## Feature Importance (Based on Stacking Model)

Here are the top features based on their importance as evaluated by the stacking regressor:

| **Feature**                                    | **Importance** |
| ---------------------------------------------- | -------------- |
| lunch_free/reduced                             | 0.0833         |
| lunch_standard                                 | 0.0768         |
| test preparation course_none                   | 0.0730         |
| race/ethnicity_group B                         | 0.0655         |
| test preparation course_completed              | 0.0638         |
| parental level of education_high school        | 0.0634         |
| parental level of education_bachelor's degree  | 0.0625         |
| race/ethnicity_group E                         | 0.0615         |
| parental level of education_some high school   | 0.0611         |
| gender_female                                  | 0.0608         |
| race/ethnicity_group C                         | 0.0586         |
| gender_male                                    | 0.0571         |
| race/ethnicity_group D                         | 0.0494         |
| parental level of education_associate's degree | 0.0491         |
| race/ethnicity_group A                         | 0.0439         |
| parental level of education_some college       | 0.0415         |
| parental level of education_master's degree    | 0.0285         |

---

## Conclusion

The analysis shows that categorical features like **gender**, **race/ethnicity**, **parental level of education**, **lunch type**, and **test preparation course** all significantly impact the average score, based on the results of ANOVA. Additionally, the correlation analysis and feature importance values highlight the most influential factors for predicting student performance.
