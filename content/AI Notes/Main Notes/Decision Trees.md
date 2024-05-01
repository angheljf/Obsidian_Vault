---
title: Decision Trees
created: 2023-08-13T20:17:00
last modified: Sunday 13th August 2023 20:17
aliases: 
tags:
  - AI
  - SL
type: Model Selection
---
- Refer to [Activity 03-Decision_Tree](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/04-Classification/demos/03-Decision_Tree) in order to see an example of how to apply a Decision Tree model.
- Initial DataFrame:
```python
# Load data
file_path = "https://static.bc-edx.com/mbc/ai/m4/datasets/crowdfunding-data.csv"
df_crowdfunding = pd.read_csv(file_path)
df_crowdfunding.head()
```
![[crowdfunding-dataframe.png]]
- Define our features and target sets:
```python
# Define features set
X = df_crowdfunding.copy()
X.drop("outcome", axis=1, inplace=True)

# Define target vector
y = df_crowdfunding["outcome"].values.reshape(-1, 1)
```
- Split data into training and testing sets:
```python
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=78)
```
- Scale the features data using the `StandardScaler`:
```python
# Create the StandardScaler instance
scaler = StandardScaler()

# Fit the StandardScaler with the training data
X_scaler = scaler.fit(X_train)

# Scale the training data
X_train_scaled = X_scaler.transform(X_train)
X_test_scaled = X_scaler.transform(X_test)
```
- Create and fit the Decision Tree model:
```python
# Create the decision tree classifier instance
model = tree.DecisionTreeClassifier()

# Fit the decision tree classifier
model = model.fit(X_trained_scaled, y_train)
```
- Validate the model using the `accuracy_score()` function:
```python
predictions = model.predict(X_test_scaled)

# Calculate the accuracy score
acc_score = accuracy_score(y_text, predictions)

print(f"Accuracy Score : {acc_score}")
```
```text
Accuracy Score : 0.9575971731448764
```
- Visualize the decision tree model using `pydotplus`:
```python
# Create DOT data
dot_data = tree.export_graphviz(
    model, out_file=None, feature_names=X.columns, class_names=["0", "1"], filled=True
)

# Draw graph
graph = pydotplus.graph_from_dot_data(dot_data)

# Show graph
Image(graph.create_png())
```
![[crowdfunding-tree.png]]
- Save the image as a PDF or PNG with `graph.write_<file_type>()`:
```python
# Save the tree as PDF
file_path = "crowdfunding_tree.pdf"
graph.write_pdf(file_path)

# Save the tree as PNG
file_path = "crowdfunding_tree.png"
graph.write_png(file_path)
```
---
>Related Notes: [[Non-linear Models]]

>Tags: #AI #SL 