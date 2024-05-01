---
title: Spending Beyond our K-Means
created: 2023-07-15T14:00:00
last modified: Saturday 15th July 2023 20:35
aliases: 
tags:
  - AI
  - UL
type: Intro
---
- Refer to [Activity 01-Spending_Beyond-Our-KMeans](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/02-Unsupervised-Learning/activities/01-Spending_Beyond_Our_KMeans) in order to see another example of customer segmentation using [[The K-Means Algorithm]].
- Initial DataFrame:
```python
# Review the DataFrame
df_shopping.head()
```
![[shopping-data-DataFrame 1.png]]
- Create function to change column "Card Type" from categorical to numerical:
```python
def encodeCard(card_type):
    """
    This function encodes a card type by setting credit card purchases to 1 and debit cards to 0.
    """
    if card_type.lower() == "credit":
        return 1
    else:
        return 0
```
- Apply function:
```python
# Edit the `Card Type` column using the encodeCard function
df_shopping["Card Type"] = df_shopping["Card Type"].apply(encodeCard)

# Review the DataFrame
df_shopping.head()
```
![[encoded-shopping-data-dataframe.png]]
- Scale "Annual Income" column:
```python
# Scale the Annual Income column
df_shopping["Annual Income"] = df_shopping["Annual Income"] / 1000

# Review the DataFrame
df_shopping.head()
```
![[scaled-shopping-data-dataframe.png]]
- Drop "CustomerID" column and create K-Means model for 4 and 5 clusters:
```python
# Initialize the K-Means model; n_clusters=4 and n_init='auto'
# For five clusters: n_clusters=5
model_k4 = KMeans(n_clusters=4, n_init='auto')

# Fit the model
model_k4.fit(df_shopping)

# Predict the model segments (clusters)
customer_segments_k4 = model_k4.predict(df_shopping)

# View the customer segments
print(customer_segments_k4)
```
```txt
[1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1 2 1
 2 1 2 1 2 1 2 1 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
 2 2 2 2 2 2 2 2 2 2 2 2 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0
 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0 3
 0 3 0 3 0 3 0 3 0 3 0 3 0 3 0]
```
- Add the predictions for four and five clusters to new DataFrame:
```python
# Create a copy of the df_shopping DataFrame and name it as df_shopping_predictions
df_shopping_predictions = df_shopping.copy()

# Create a new column in the DataFrame with the predicted clusters with k=4
df_shopping_predictions["Customer Segment (k=4)"] = customer_segments_k4

# Create a new column in the DataFrame with the predicted clusters with k=5
df_shopping_predictions["Customer Segment (k=5)"] = customer_segments_k5

# Review the DataFrame
df_shopping_predictions.head()
```
![[prediction-shopping-data-dataframe.png]]
- Plots with `n_clusters` equal to 4 and 5 respectively:
```python
# Create a scatter plot with with x="Annual Income" and y="Spending Score" with k=4 segments
df_shopping_predictions.plot.scatter(
    x="Annual Income",
    y="Spending Score",
    c="Customer Segment (k=4)",
    title = "Scatter Plot by Stock Segment - k=4",
    colormap='winter'
)
```
![[four-clusters-shopping-data.png]]
```python
# Create a scatter plot with x="Annual Income" and y="Spending Score" with k=5 segments
df_shopping_predictions.plot.scatter(
    x="Annual Income",
    y="Spending Score",
    c="Customer Segment (k=5)",
    title = "Scatter Plot by Stock Segment - k=5",
    colormap='winter'
)
```
![[five-clusters-shopping-data.png]]

---
>Related Notes: [[Clustering]], [[Using the K-Means Algorithm]]

>Tags: #AI  #UL
