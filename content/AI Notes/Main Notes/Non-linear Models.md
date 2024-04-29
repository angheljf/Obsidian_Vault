---
title: Non-linear Models
created: 2023-08-12T21:08:00
last modified: Saturday 12th August 2023 19:08
aliases: 
tags:
  - AI
  - SL
type: Model Selection
---
- We will examine two non-linear models:
	- **Non-linear SVM**
	- **Decision Trees**
- Non-linear SVM separates data points using a circular hyperplane in three-dimensional space.
- Decision trees can be used in two ways:
	- To model multi-class classification systems.
	- To improve the accuracy of predictions.
- The scatter plot appears in separate layers between which we can establish a hyperplane as illustrated in the following image:
![[nonlinear-circle-plot-3d.png]]
- Decision tree learning is a method for encoding a series of true–false questions to map non-linear relationships in data.
- There are some key concepts that are important to know while working with decision trees:
	- **Root node:** Represents the entire population or sample data. This node gets divided into two or more homogeneous sets.
	- **Parent node:** A node that is divided into.
	- **Child node:** Subnode of a parent node.
	- **Decision node:** A parent node with at least one child node that is a terminal node.
	- **Leaf or terminal node:** A node that does not split.
	- **Branch or subtree:** A subsection of the entire tree.
	- **Splitting:** The process of dividing a node into two or more subnodes.
	- **Pruning:** The process of removing subnodes of a decision node.
	- **Tree depth:** The number of decision nodes encountered before making a decision.
- The following image illustrates these concepts, with the exception of pruning:
![[decision-tree-nodes.png]]
---
>Related Notes: [[Linear vs Non-linear Data]]
>Tags: #AI #SL 
