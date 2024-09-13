---
title: Save and Load a Deep Learning Model
created: 2024-09-13T19:38:00
last modified: 2024-09-13 19:38
aliases: 
tags:
  - AI
  - NN
type: Deep Learning
---
- For simple modeling problems like the ones covered in this module, we can train a model in the same notebook in which we analyze our data.
- However, for more formal applications, data scientists can't afford the time or the resources to build and train a model each time they analyze data.
- Data scientists must store and access trained models outside of the training environment.
- As usual, the key to doing this lies in using Keras. The `Sequential` model has a `save` function that can export an entire model to a Hierarchical Data Format [(HDF5)](https://en.wikipedia.org/wiki/Hierarchical_Data_Format "https://en.wikipedia.org/wiki/Hierarchical_Data_Format") file. The `save` function exports the following aspects of the model:
	- The configuration of the model layers;
	- The weights associated with each layer;
	- The activation functions;
	- The optimizer; and
	- The set of losses and metrics.
- Once the model has been saved, anyone can use the `load_model` function in Keras to import the exact same trained model to their environment.
- Let's demonstrate how to export and import a neural network model using the wine quality model we built.
- Save the model as an HDF5 file:
```python
# Set the model's file path
file_path = Path("saved_models/wine_quality.h5")

# Export your model to an HDF5 file
nn.save(file_path)
```
- Load the saved model:
```python
# Import the required libraries
import tensorflow as tf

# Set the model's file path
file_path = Path("Resources/wine_quality.h5")

# Load the model to a new object
nn_imported = tf.keras.models.load_model(file_path)
```
- Test the model's performance:
```python
# Evaluate the model using the test data
model_loss, model_accuracy = nn_imported.evaluate(X_test_scaled, y_test, verbose=2)

# Display evaluation results
print(f"Loss: {model_loss}, Accuracy: {model_accuracy}")
```
![[evaluating-imported-model.png]]
- Our imported model produces the same performance metrics as the original model.
- Using this same procedure, we can import any Keras neural network model.
---
>Related Notes: [[Test and Evaluate a Deep Learning Model]]

>Tags: #AI #NN 
