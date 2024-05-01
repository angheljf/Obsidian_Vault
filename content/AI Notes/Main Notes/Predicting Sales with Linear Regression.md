---
title: Predicting Sales with Linear Regression
created: 2023-09-01T19:08:00
last modified: Tuesday 1st August 2023 19:08
aliases: 
tags:
  - AI
  - SL
type: Linear Regression
---
- Refer to [Activity 01-Linear_Regression](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/03-Regression/activities/01-Linear_Regression) in order to create a linear regression model, make predictions about expected sales and evaluate the model by calculating MSE, RMSE and R<sup>2</sup>.
- Initial DataFrame:
```python
# Read the sales data
file_path = "https://static.bc-edx.com/mbc/ai/m3/datasets/sales.csv"
df_sales = pd.read_csv(file_path)

# Display sample data
df_sales.head()
```
![[sales-dataframe.png]]
- Plot our data:
```python
# Create a scatter plot with the sales information
sales_plot = df_sales.plot.scatter(
        x="ads",
        y="sales",
        title="Sales per Number of Ads"
    )
sales_plot
```
![[sales-scatterplot.png]]
- Create our `X` and `y` variables for the linear model:
```python
# Create the X set by using the `reshape` function to format the ads data as a single column array.
X = df_sales["ads"].values.reshape(-1, 1)
    
# Display sample data
X[:5]
```
```text
array([[ 21],
       [180],
       [ 50],
       [195],
       [ 96]])
```
```python
y = df_sales['sales']
```
- Start the **model-fit-predict** process:
```python
# Create a model with scikit-learn
model = LinearRegression()

# Fit the data into the model
model.fit(X,y)
```
- Extract information about the best fit line formula:
```python
# Display the slope
print(f"Model's slope: {model.coef_}")
```
```text
Model's slope: [81.34898394]
```
```python
# Display the y-intercept
print(f"Model's y-intercept: {model.intercept_}")
```
```text
Model's y-intercept: 7764.796945240409
```
- Put these elements together to print the model’s best fit line formula:
```python
# Display the model's best fit line formula
print(f"Model's formula: y = {model.intercept_} + {model.coef_[0]}X")
```
```text
Model's formula: y = 7764.796945240409 + 81.34898393753781X
```
- Use the `predict` function to make predictions by using the original data, `X`:
```python
# Make predictions using the X set
predicted_y_values = model.predict(X)
```
- Create a new DataFrame with the original data and the predicted values:
```python
# Create a copy of the original data
df_sales_predicted = df_sales.copy()
    
# Add a column with the predicted sales values
df_sales_predicted["sales_predicted"] = predicted_y_values

# Display sample data
df_sales_predicted.head()
```
![[sales-predicted-dataframe.png]]
- Plot our best fit line:
```python
# Create a line plot of the predicted salary values
best_fit_line = df_sales_predicted.plot.line(
    x = "ads",
    y = "sales_predicted",
    color = "red"
)

best_fit_line
```
![[sales-best-fit-line.png]]
- Plot the best fit line over the original data:
```python
# Superpose the original data and the best fit line
# Create a scatter plot with the sales information
sales_plot = df_sales_predicted.plot.scatter(
    x="ads",
    y="sales",
    title="Sales per Number of Ads"
)

    best_fit_line = df_sales_predicted.plot.line(
    x = "ads",
    y = "sales_predicted",
    color = "red",
    ax=sales_plot
)
sales_plot
```
![[sales-best-fit-and-scatter-plot.png]]
- Make predictions manually by using the model’s best fit line equation:
```python
# Display the formula to predict the sales with 100 ads
print(f"Model's formula: y = {model.intercept_} + {model.coef_[0]} * 100")
    
# Predict the sales with 100 ads
y_100 = model.intercept_ + model.coef_[0] * 100

# Display the prediction
print(f"Predicted sales with 100 ads: ${y_100:.2f}")
```
```text
Model's formula: y = 7764.796945240409 + 81.34898393753781 * 100
Predicted sales with 100 ads: $15899.70
```
- Use the `predict` function to make multiple predictions at the same time:
```python
# Create an array to predict sales for 100, 150, 200, 250, and 300 ads
X_ads = np.array([100, 150, 200, 250, 300])

# Format the array as a one-column array
X_ads = X_ads.reshape(-1,1)

# Predict sales for 100, 150, 200, 250, and 300 ads
predicted_sales = model.predict(X_ads)
```
- Create a DataFrame to visualize the forecasted sales:
```python
# Create a DataFrame for the predicted sales
    df_predicted_sales = pd.DataFrame(
    {
            "ads": X_ads.reshape(1, -1)[0],
            "predicted_sales": predicted_sales
    }
)

# Display data
df_predicted_sales
```
![[df-predicted-sales-dataframe.png]]
- Evaluate the liner regression model:
```python
# Import relevant metrics - score, r2, mse, rmse - from Scikit-learn
from sklearn.metrics import mean_squared_error, r2_score

# Compute the metrics for the linear regression model
score = round(model.score(X, y, sample_weight=None),5)
r2 = round(r2_score(y, predicted_y_values),5)
mse = round(mean_squared_error(y, predicted_y_values),4)
rmse = round(np.sqrt(mse),4)
    
# Print relevant metrics.
print(f"The score is {score}.")
print(f"The r2 is {r2}.")
print(f"The mean squared error is {mse}.")
print(f"The root mean squared error is {rmse}.")
```
```text
The score is 0.922.
The r2 is 0.922.
The mean squared error is 1922652.7854.
The root mean squared error is 1386.5976.
```

---
>Related Notes: [[Making Predictions with Linear Regression]], [[Model Evaluation - Quantifying Regression]]

>Tags: #AI #SL 
