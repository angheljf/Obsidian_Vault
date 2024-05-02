---
title: Making an Artificial Brain
created: 2024-05-01T11:31:00
last modified: 2024-05-01 11:30
aliases: 
tags:
  - AI
  - NN
type: Neural
---
- The computational equivalent of a single neuron in the brain is called a **perceptron**.
- Just as the neurons in your brain used input signals to classify things, perceptrons also make classification decisions based on input.
![[perceptron.png]]
- A perceptron is a **binary** classifier, which means that it can classify the input data it receives into two parts by assigning it a numerical value of either 1 or 0.
- The perceptron works as follows:
	- The perceptron receives any number of inputs ***x***<sub>n</sub> in numeric form.
	- The inputs are then multiplied by a numeric value called a **weight** (***w<sub>n</sub>***).
	- The weighted values (***x<sub>i</sub> * w<sub>i</sub>***) are then added together to produce the **weighted sum**. Included in the weighted sum is a numerical value called a **bias** represented by ***w<sub>0</sub>***.
	- The final component of the perceptron is the **activation function**. 
- In summary, a perceptron is a foundational unit of a neural network that receives input signals, applies weights, a bias and an activation function to achieve a binary output.
---
>Related Notes: [[What is a Neural Network]]

>Tags: #AI #NN 
