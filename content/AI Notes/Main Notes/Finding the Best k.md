---
title: Finding the Best k
created: 2023-07-16T20:03:00
last modified: Thursday 20th July 2023 11:54
aliases: 
tags:
  - AI
  - UL
type: Clustering
---
- Refer to [Activity 02-Finding_the_Best_k](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/02-Unsupervised-Learning/activities/02-Finding_the_Best-k) in order to see an example of applying the [[The Elbow Method]].
- Compute the inertia for each value of `k`:
 ```python
# Create a list for the range of k's to analyze in the elbow plot
# The range should be 1 to 11.
k = list(range(1, 11))

# Create an empty list to hold inertia scores
inertia = []

# For each k, define and fit a K-means model and append its inertia to the above list
for i in k:
    model = KMeans(n_clusters=i, n_init='auto', random_state=0)
    model.fit(df_options)
    inertia.append(model.inertia_)

# View the inertia list
inertia
```
```txt
[10804651.95737489,
 3367798.734774582,
 1660546.9227245785,
 1247312.1570758787,
 935906.6738774017,
 869521.614591255,
 784817.4155094068,
 701355.5914609156,
 625262.9863095116,
 578651.2374997162]
```
- `k` and inertia values DataFrame:
```python
# Create a dictionary with the data to plot the Elbow curve
elbow_data = {
    "k": k,
    "inertia": inertia
}

# Create a DataFrame from the dictionary holding the values for k and inertia.
df_elbow_data = pd.DataFrame(elbow_data)
df_elbow_data
```
![[k-and-inertia-values-dataframe.png]]
- Plot the Elbow curve:
```python
# Plot the elbow curve using Pandas Plot.
df_elbow_data.plot.line(
    x="k",
    y= "inertia",
    title="Elbow Curve",
    xticks=k
)
```
![[k-and-inertia-values-plot.png]]
- Based on the plot, 3 seems to be the optimal number for the value of `k`.
---
>Related Notes: [[The Elbow Method]], [[Apply the Elbow Method]]
>Tags: #AI #UL 
