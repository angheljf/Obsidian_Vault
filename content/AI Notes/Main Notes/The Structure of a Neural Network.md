---
title: The Structure of a Neural Network
created: 2024-05-01T20:45:00
last modified: 2024-05-01 20:45
aliases: 
tags:
  - AI
  - NN
type: Neural
---
- Perceptrons interact with one another in a **neural network**.
- A neural network consists of three layers, each of which is connected to and learns from the others:
	- The first layer is the **input layer**. This is where the network receives input values and then transforms them by weighting them through multiplication.
	- The second layer is the **hidden** layer, which can consist of one or more perceptrons.
	- The third layer is the **output** layer, which reports the outcome of the neural network.
## Activation Functions
---
- The **activation function** is applied to the end of each individual perceptron.
- It transforms the output into a quantitative value, which may be a continuous or binary value.
- The transformed output value is in turn used as an input for the next perceptron in the neural network.
- When designing a neural network, developers usually test different activation function combinations to determine which function works best for the case at hand.
- [Here](https://ml-cheatsheet.readthedocs.io/en/latest/activation_functions.html) is the documentation for the different activation functions that can be applied to a neural network.
---
>Related Notes: [[What is a Neural Network]]

>Tags: #AI #NN 
