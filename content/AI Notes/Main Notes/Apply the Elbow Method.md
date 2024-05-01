---
title: Apply the Elbow Method
created: 2023-07-16T19:15:00
last modified: Thursday 20th July 2023 11:54
aliases: 
tags:
  - AI
  - UL
type: Clustering
---
- Refer to [Activity 03-Elbow_Method](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/02-Unsupervised-Learning/demos/03-Elbow_Method) in order to see an example of how to use [[The Elbow Method]].
- Initial DataFrame:
```python
df_shopping.head()
```
![[shopping-data-DataFrame 1.png]]
- Compute the inertia for each value of `k`:
```python
# Create an empty list to store the inertia values
inertia = []

# Create a list with the number of k-values to try
k = list(range(1, 11))

# Create a for loop to compute the inertia with each possible value of k and add the values to the inertia list.
for i in k:
    model = KMeans(n_clusters=i, n_init='auto', random_state=1)
    model.fit(df_shopping)
    inertia.append(model.inertia_)
```
- Inertia DataFrame:
```python
# Create a Dictionary that holds the list values for k and inertia
elbow_data = {
    "k": k,
    "inertia": inertia}

# Create a DataFrame using the elbow_data Dictionary
df_elbow = pd.DataFrame(elbow_data)

# Review the DataFrame
df_elbow.head()
```
![[elbow-data-DataFrame.png]]
- Plot the Elbow chart:
```python
# Plot the Elbow curve
df_elbow.plot.line(
    x="k",
    y="inertia",
    title="Elbow Curve",
    xticks=k)
```
![[elbow-chart.png]]
- Determine the rate of decrease:
```python
# Determine the rate of decrease between each k-value
k = elbow_data["k"]
inertia = elbow_data["inertia"]
for i in range(1, len(k)):
    percentage_decrease = (inertia[i-1] - inertia[i]) / inertia[i-1] * 100
    print(f"Percentage decrease from k={k[i-1]} to k={k[i]}: {percentage_decrease:.2f}%")
```
- The output shows the rate of decrease between each k-value and that the rate of decrease in inertia **begins** to slow down between `k=4` and `k=5`.
```text
Percentage decrease from k=1 to k=2: 27.12%
Percentage decrease from k=2 to k=3: 29.57%
Percentage decrease from k=3 to k=4: 34.14%
Percentage decrease from k=4 to k=5: 27.65%
Percentage decrease from k=5 to k=6: 22.74%
Percentage decrease from k=6 to k=7: 11.81%
Percentage decrease from k=7 to k=8: 6.33%
Percentage decrease from k=8 to k=9: 4.82%
Percentage decrease from k=9 to k=10: 7.75%
```
- Note that an elbow curve is **not** a definite answer for how many clusters there should be. Rather, it works as a guide and it’s ultimately up to you to determine the right amount.
---
>Related Notes: [[Clustering]], [[The Elbow Method]]

>Tags: #AI #UL 
