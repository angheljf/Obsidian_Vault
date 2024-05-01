---
title: Making Predictions with Linear Regression
created: 2023-07-29T20:23:00
last modified: Saturday 29th July 2023 20:23
aliases: 
tags:
  - AI
  - SL
type: Linear Regression
---
- Refer to [Activity 01-Linear_Regression](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/03-Regression/demos/01-Linear_Regression) in order to see an example of the basic procedure to implement a supervised learning model.
- Initial DataFrame:
```python
# Read salary data
file_path = "https://static.bc-edx.com/mbc/ai/m3/datasets/salary-data.csv"
df_salary = pd.read_csv(file_path)

# Display sample data
df_salary.head()
```
![[salary-dataframe-head.png]]
- Inspect the relationship between "years_experience" and "salary":
```python
# Create a scatter plot with the salary information
salary_plot = df_salary.plot.scatter(
    x="years_experience",
    y="salary",
    title="Expected Salary Based on Years of Experience"
)

salary_plot
```
![[salary-scatter-plot.png]]
- Format data to meet Scikit-learn library:
```python
# Reformat data of the independent variable X as a single-column array
# First argument of reshape specifies the rows. -1 = unspecified
# Second argument of reshape specifies the columns. 1 = one column
# Output is a 2-dimensional array
X = df_salary["years_experience"].values.reshape(-1, 1)

X[:5]
```
```text
array([[1.1],
       [1.3],
       [1.5],
       [2. ],
       [2.2]])
```
- Assign the target variable to `y`:
```python
# Create an array for the dependent variable y
y = df_salary["salary"]
```
- Create an instance of the linear regression model:
```python
model = LinearRegression()
```
- Fit the data:
```python
model.fit(X, y)
```
- Examine the slope and y-intercept of the model:
```python
# Display the slope
print(f"Model's slope: {model.coef_}")
```
```text
Model's slope: [9449.96232146]
```
```python
# Display the y-intercept
print(f"Model's y-intercept: {model.intercept_}")
```
```text
Model's y-intercept: 25792.20019866871
```
- Build the formula for our model’s line of best fit:
```python
# Display the model's best fit formula
print(f"Model's formula: y = {model.intercept_} + {model.coef_[0]}X")
```
```text
Model's formula: y = 25792.20019866871 + 9449.962321455074X
```
- Predicting the salary of a person with 7 years of experience:
```python
# Display the formula to predict the salary for a person with 7 years of experience
print(f"Model's formula: y = {model.intercept_} + {model.coef_[0]} * 7")

# Predict the salary for a person with 7 years of experience
y_7 = model.intercept_ + model.coef_[0] * 7

# Display the prediction
print(f"Predicted salary for a person with 7 years of experience: ${y_7:.2f}")
```
```text
Model's formula: y = 25792.20019866871 + 9449.962321455074 * 7
Predicted salary for a person with 7 years of experience: $91941.94
```
- Use `predict()` method to generate predictions:
``` python
# Make predictions using the X set
predicted_y_values = model.predict(X)
```
- Create new DataFrame with the predicted values:
```python
# Create a copy of the original data
df_salary_predicted = df_salary.copy()

# Add a column with the predicted salary values
df_salary_predicted["salary_predicted"] = predicted_y_values

# Display sample data
df_salary_predicted.head()
```
![[salary-predicted-dataframe.png]]
- Plot line of best fit, also known as the regression line:
```python
# Create a line plot of the predicted salary values
best_fit_line = df_salary_predicted.plot.line(
    x = "years_experience",
    y = "salary_predicted",
    color = "red"
)

best_fit_line
```
![[salary-predicted-best-fit-line.png]]
- Plot the predictions as a red line against the original data points:
```python
# Plot salary scatter and line of best fit together
salary_plot = df_salary_predicted.plot.scatter(
    x="years_experience",
    y="salary",
    title="Expected Salary Based on Years of Experience"
)

# Create a line plot of the predicted salary values
best_fit_line = df_salary_predicted.plot.line(
    x = "years_experience",
    y = "salary_predicted",
    color = "red",
    ax=salary_plot
)

salary_plot

```
![[salary-plot-with-regression-line.png]]

---
>Related Notes: [[Intro to Linear Regression]]

>Tags: #AI #SL 
