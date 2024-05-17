---
title: Train a Deep Learning Model
created: 2024-05-17T11:57:00
last modified: 2024-05-17 11:57
aliases: 
tags:
  - AI
  - NN
type: Deep Learning
---
- Now, we will compile and fit our deep neural network model:
```python
# Compile the model
nn.compile(loss="mean_squared_error", optimizer="adam", metrics=["mse"])

# Fit the model
deep_net_model = nn.fit(X_train_scaled, y_train, epochs=100)
```
- Recall that epochs can be loosely defined as one iteration of a neural network model— that is, one pass of the entire training dataset through the model. The loss function scores the model’s performance after each new epoch. The optimizer shapes and molds the model while it’s trained on the data. And finally, the evaluation metric assesses the model’s performance.
- We are using `mse` in this case instead of `accuracy` because `mse` is a better evaluation metric for regression models.
- The closer to zero the MSE value is, the better the performance of the model.
- We also used `mean_squared_error` as the loss function since it is better for regression models.
---
>Related Notes: [[Create a Deep Learning Model]]

>Tags: #AI #NN 
