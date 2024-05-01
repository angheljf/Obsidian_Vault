---
title: Apply Standard Scaling
created: 2023-07-17T10:42:00
last modified: Monday 17th July 2023 10:42
aliases: 
tags:
  - AI
  - UL
type: Clustering
---
- Refer to [Activity 04-Standard_Scaling](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/02-Unsupervised-Learning/demos/04-Standard_Scaling) in order to see an example of how to apply standard scaling.
- Initial DataFrame:
```python
df_shopping.head()
```
![[shopping-data-DataFrame.png]]
- Scaling the data:
```python
# Scaling the numeric columns
shopping_data_scaled = StandardScaler().fit_transform(df_shopping[["Age", "Annual Income", "Spending Score"]])
# Creating a DataFrame with the scaled data
df_shopping_transformed = pd.DataFrame(shopping_data_scaled, columns=["Age", "Annual Income", "Spending Score"])
# Display sample data
df_shopping_transformed.head()
```
![[scaled-shopping-data.png]]
- Using `get_dummies` to transform the categorical column "Card Type":
```python
# Transform the Card Type column using get_dummies()
card_dummies = pd.get_dummies(df_shopping["Card Type"])
# Display sample data
card_dummies.head()
```
![[transformed-scaled-data.png]]
- Concatenate (or combine) both DataFrames using `concat`:
```python
# Concatenate the df_shopping_transformed and the card_dummies DataFrames
df_shopping_transformed = pd.concat([df_shopping_transformed, card_dummies], axis=1)
# Display sample data
df_shopping_transformed.head()
```
![[concatenated-transformed-DataFrame.png]]

---
>Related Notes: [[Scaling and Transforming for Optimization]]

>Tags: #AI #UL 
