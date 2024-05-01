---
title: Using the K-Means Algorithm
created: 2023-07-15T12:00:00
last modified: Thursday 20th July 2023 11:54
aliases: 
tags:
  - AI
  - UL
type: Intro
---
- Refer to [Activity 02-Kmeans](C:\Users\JORMIL\Work\AI_MicroBootCamp\mbc-ai\02-Unsupervised-Learning\demos\02-Kmeans) in order to see an example of customer segmentation using [[The K-Means Algorithm]].
- Initial DataFrame:
```python
# Read in the CSV file as a Pandas DataFrame
service_ratings_df = pd.read_csv("https://static.bc-edx.com/mbc/ai/m2/datasets/service-ratings.csv")

# Review the DataFrame
service_ratings_df.head()
```
![[service-ratings-DataFrame.png]]
- Plot the data on a scatter plot:
![[service-ratings-scatter-plot.png]]
- Create K-means model:
```python
# Create and initialize the K-means model instance for 2 clusters
model = KMeans(n_clusters=2, n_init='auto', random_state=1)
```
- Fit model  and make predictions using our DataFrame:
```python
# Fit the data to the instance of the model
model.fit(service_ratings_df)

# Make predictions about the data clusters using the trained model
customer_ratings = model.predict(service_ratings_df)

# Print the predictions
print(customer_ratings)
```
![[customer-ratings-predictions-array.png]]
- Add predictions to new DataFrame:
```python
# Create a copy of the DataFrame
service_rating_predictions_df = service_ratings_df.copy()

# Add a column to the DataFrame that contains the customer_ratings information
service_rating_predictions_df['customer rating'] = customer_ratings

# Review the DataFrame
service_rating_predictions_df.head()
```
![[customer-ratings-predictions-DataFrame.png]]
- Plot the results of the new DataFrame:
```python
# Plot the data points based on the customer rating
service_rating_predictions_df.plot.scatter(
    x="mobile_app_rating",
    y="personal_banker_rating",
    c="customer rating",
    colormap='winter')
```
![[customer-ratings-predictions-scatter-plot.png]]

---
>Related Notes: [[Clustering]], [[Using the K-Means Algorithm]]

>Tags: #AI #UL 
