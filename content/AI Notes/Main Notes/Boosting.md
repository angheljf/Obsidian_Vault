---
title: Boosting
created: 2023-08-20T21:34:00
last modified: Sunday 20th August 2023 21:34
aliases: 
tags:
  - AI
  - SL
type: Ensemble Learning
---
- **Boosting** is a aggregation method where individual weak learners get "boosted" if they are contributing correct solutions, but get diminished if they are not.
- Boosting methods can be used for regression and classification problems.
- To reduce bias, we train the model to recognize errors and avoid them in the next iteration.
- To do so, we follow three steps that distinguish boosting from random forest:
	- **Assign weights**: A sample that is more difficult to predict is assigned a higher weight since the model must work harder to make a correct prediction.
	- **Pay attention to the weights**: We create an algorithm that incorporates the weight assigned to each sample. This enables the learner to make correct predictions for data with heavier weights.
	- **Add learners sequentially**: This means that the model starts with one decision tree, then the weights are updated for the wrongly classified observations. The new weights are fed into the next model. Again, we update any wrongly classified weights and feed them into a third model. Each successive model is considered a weak model. This continues until the model minimizes errors and correctly predicts the dataset.
- Three forms of boosting are common in machine learning:
	- **AdaBoost**: Trains itself iteratively, giving higher weight to the weak learners where it incorrectly predicted observations.
	- **Gradient Boosting**: Gradient boosting iteratively trains an ensemble of shallow decision trees by using the pseudo residuals (i.e., interim errors between the model output and actual variable) to make predictions.
	- **XGBoost**: A software library that optimizes computational speed and model performance. It does this by building boosted trees in parallel.
---
>Related Notes: [[Intro to Ensemble Learning]], [[Random Forest]]
>Tags: #AI #SL 
