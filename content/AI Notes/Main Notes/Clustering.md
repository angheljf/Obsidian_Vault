---
title: Clustering
created: 2023-07-15T11:00:00
last modified: Thursday 20th July 2023 11:53
aliases: 
tags:
  - AI
  - UL
type: Intro
---
- Clustering is the process of grouping data together based on a particular similarity.
- The process of clustering data points into groups is called **centering**. Centering helps to determine the number of classes or groups to create.
- Example:
```python
# Import dependencies
from sklearn.datasets import make_blobs
import pandas as pd

# Generate three synthetic clusters
X, y = make_blobs(
    centers=3,
    n_features=2,
    random_state=1
    )

# Transform the y variables into a single column.
y = y.reshape(-1, 1)

# Create a DataFrame with the synthetic data
df = pd.DataFrame(X, columns=["Feature 1", "Feature 2"])

# Add the y variables as the "Target" column.
df["Target"] = y

# Visualize the data
df.plot.scatter(x="Feature 1",
                y="Feature 2",
                c="Target",
                colormap="winter")
```

![[make-blobs-three-clusters.png]]

---
>Related Notes:
 
>Tags: #AI #UL