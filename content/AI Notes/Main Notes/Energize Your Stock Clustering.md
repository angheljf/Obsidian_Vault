---
title: Energize Your Stock Clustering
created: 2023-07-21T23:07:00
last modified: Friday 21st July 2023 23:07
aliases: 
tags:
  - AI
  - UL
type: PCA
---
- Refer to [Activity 04-Energize_Your_Stock_Clustering](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/02-Unsupervised-Learning/activities/04-Energize_Your_Stock_Clustering) in order to see an example of how to use the K-means algorithm and clustering optimization techniques to cluster stocks.
- **Note**: This is a continuation of activity [[Standardizing Stock Data]]
- Scaled DataFrame with clusters:
![[energize-scaled-prediction-dataframe.png]]
- Plot the predicted clusters:
![[energize-scaled-prediction-plot.png]]
- Reduce the number of features by creating a PCA model:
```python
# Create the PCA model instance where n_components=2
pca = PCA(n_components=2)

# Fit the df_stocks_scaled data to the PCA
stocks_pca_data = pca.fit_transform(df_stocks_scaled)

# Review the first five rows of the PCA data using bracket notation ([0:5])
stocks_pca_data[:5]
```
```txt
array([[-2.00255809,  0.65050845],
       [-1.64406859, -1.58484859],
       [ 1.86569239,  1.41737226],
       [-2.28149773,  1.92052319],
       [-3.05864989,  2.34785522]])
```
- Retrieve the explained variance:
```python
# Calculate the explained variance
pca.explained_variance_ratio_
```
```txt
array([0.6236361 , 0.17105473])
```
- Create DataFrame that contains the principal components and the “Ticker” column as the index:
```python
# Creating a DataFrame with the PCA data
df_stocks_pca = pd.DataFrame(stocks_pca_data, columns=["PC1", "PC2"])

# Copy the tickers names from the original data
df_stocks_pca["Ticker"] = df_stocks.index  

# Set the Ticker column as index
df_stocks_pca = df_stocks_pca.set_index("Ticker")

# Review the DataFrame
df_stocks_p
```
![[stocks-pca-dataframe.png]]
- Re-run the K-means algorithm on the PCA DataFrame:
```python
# Initialize the K-Means model with n_clusters=3
model = KMeans(n_clusters=3, n_init='auto')

# Fit the model for the df_stocks_pca DataFrame
model.fit(df_stocks_pca)

# Predict the model segments (clusters)
stock_clusters = model.predict(df_stocks_pca)

# View the stock segments
print(stock_clusters)
```
```txt
[1 0 2 1 1 2 1 0 0 2 0 0 1 0 0 0 2 0 1 2 2 2 2 1]
```
- Create a copy of the PCA DataFrame and add the predicted cluster data:
```python
# Create a copy of the df_stocks_pca DataFrame and name it as df_stocks_pca_predictions
df_stocks_pca_predictions = df_stocks_pca.copy()

# Create a new column in the DataFrame with the predicted clusters
df_stocks_pca_predictions["StockCluster"] = stock_clusters

# Review the DataFrame
df_stocks_pca_predictions.head()
```
![[predictions-stock-pca-dataframe.png]]
- Plot the clusters:
```python
# Create the scatter plot with x="PC1" and y="PC2"
df_stocks_pca_predictions.plot.scatter(
    x="PC1",
    y="PC2",
    c="StockCluster",
    colormap='winter',
    title = "Scatter Plot by Stock Segment - PCA=2"
)
```
![[predictions-stock-pca-plot.png]]

---
>Related Notes: [[Intro to Principal Component Analysis]], [[Standardizing Stock Data]]
>Tags: #AI #UL 
