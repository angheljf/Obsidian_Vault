---
title: Understanding Categorical Data
created: 2023-08-04T20:22:00
last modified: Friday 4th August 2023 20:22
aliases: 
tags:
  - AI
  - SL
type: Classification
---
- Refer to [Activity 01-Logistic_Regression](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/04-Classification/demos/01-Logistic_Regression) in order to see an example of how to create a logistic regression model.
- Import and visualize the data:
```python
import pandas as pd

# Import the data
startup_path = "https://static.bc-edx.com/mbc/ai/m4/datasets/start-up-success.csv"
df = pd.read_csv(startup_path)

# Plot the data on a scatter plot
df.plot.scatter(
    x='Industry Health',
    y='Financial Performance',
    c='Firm Category',
    marker='o',
    s=25,
    edgecolor='k',
    colormap="winter"
    )
```
![[logistic-regression-demo-plot.png]]
- In the image, the healthy firms appear in the top-right part of the plot in green and the unhealthy firms appear in the bottom-left part of the plot in blue.
---
>Related Notes: 
>Tags: #AI #SL 
