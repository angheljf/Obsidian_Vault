---
title: Standardizing Stock Data
created: 2023-07-17T11:24:00
last modified: Monday 17th July 2023 11:56
aliases: 
tags:
  - AI
  - UL
type: Clustering
---
- Refer to [Activity 03-Standardizing_Stock_Data](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/02-Unsupervised-Learning/activities/03-Standardizing_Stock_Data) in order to see an example of how to standardize stock data and use the K-means algorithm to cluster the data.
- Initial DataFrame:
```python
df_stocks.head()
```
![[energy-stock-dataframe.png]]
- Scale all columns except "EnergyType":
```python
# Use the StandardScaler module and fit_transform function to scale all columns with numerical values.
stock_data_scaled = StandardScaler().fit_transform(df_stocks[["MeanOpen", "MeanHigh", "MeanLow",  "MeanClose","MeanVolume", "AnnualReturn", "AnnualVariance"]] )

# Display the first five rows of the scaled data
stock_data_scaled[0:5]
```
![[scaled-energy-stocks.png]]
- Create a new DataFrame that contains the scaled data with the appropriate columns, and the index as the “Ticker” column.
```python
# Create a DataFrame called with the scaled data
# The column names should match those referenced in the StandardScaler step
df_stocks_scaled = pd.DataFrame(stock_data_scaled, columns=["MeanOpen", "MeanHigh", "MeanLow", "MeanClose", "MeanVolume", "AnnualReturn", "AnnualVariance"])

# Create a Ticker column in the df_stocks_scaled DataFrame
# using the index of the original df_stocks DataFrame
df_stocks_scaled["Ticker"] = df_stocks.index

# Set the newly created Ticker column as index of the df_stocks_scaled DataFrame
df_stocks_scaled = df_stocks_scaled.set_index("Ticker")

# Review the DataFrame
df_stocks_scaled.head()
```
![[scaled-energy-stock-dataframe.png]]
- Encode the “EnergyType” column with `get_dummies`:
```python
# Encode (convert to dummy variables) the EnergyType column
df_oil_dummies = pd.get_dummies(df_stocks["EnergyType"])
# Review the DataFrame
df_oil_dummies.head()
```
![[encoded-dataframe.png]]
- Concatenate both DataFrames:
```python
# Concatenate the `EnergyType` encoded dummies with the scaled data DataFrame
df_stocks_scaled = pd.concat([df_stocks_scaled, df_oil_dummies], axis=1)

# Display the sample data
df_stocks_scaled.head()
```
![[scaled-encoded-dataframe.png]]
- Initialize the K-means model with 3 clusters, fit the model, and make the predictions:
```python
# Initialize the K-Means model with n_clusters=3
model = KMeans(n_clusters=3, n_init='auto')

# Fit the model for the df_stocks_scaled DataFrame
model.fit(df_stocks_scaled)

# Predict the model segments (clusters)
stock_clusters = model.predict(df_stocks_scaled)

# View the stock segments
print(stock_clusters)
```
```
[1 1 0 2 2 0 1 1 1 0 1 0 1 1 1 0 0 1 1 0 0 0 0 2]
```
- Add the predictions to a copy of our concatenated DataFrame:
```python
# Create a copy of the concatenated DataFrame
df_stocks_scaled_predictions = df_stocks_scaled.copy()

# Create a new column in the copy of the concatenated DataFrame with the predicted clusters
df_stocks_scaled_predictions["StockCluster"] = stock_clusters

# Review the DataFrame
df_stocks_scaled_predictions.head()
```
![[scaled-prediction-dataframe.png]]
- Note: The `k` was given to us but we could have used [[The Elbow Method]] in order to find the best `k`.
---
>Related Notes: [[Apply Standard Scaling]], [[The Elbow Method]], [[Apply the Elbow Method]]
>Tags: #AI #UL 
