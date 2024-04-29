---
title: Intro to Principal Component Analysis
created: 2023-07-17T11:54:00
last modified: Monday 17th July 2023 11:54
aliases: 
tags:
  - AI
  - UL
type: PCA
---
- **Principal component analysis (PCA)** is a statistical technique that we use to speed up machine learning algorithms when too many features, or dimensions, exist.
- **Dimensionality reduction** is the transformation of a large set of features into a smaller one that contains most of the information in the original, large set. This entails reducing the number of columns in a DataFrame while preserving as much useful information as possible from all the original columns. This technique increases interpretability and minimizes information loss.
- Refer to [Activity 05-Segmenting_Credit_PCA](file:///C:/Users/JORMIL/Work/AI_MicroBootCamp/mbc-ai/02-Unsupervised-Learning/demos/05-Segementing_Credit_PCA) in order to see an example of how to use PCA.
- Initial DataFrame:
```python
# Read in the CSV file as a Pandas DataFrame
ccinfo_default_df = pd.read_csv("https://static.bc-edx.com/mbc/ai/m2/datasets/ccinfo-transformed.csv")
ccinfo_default_df.head()
```
![[credit-card-info-DataFrame.png]]
- Plot the clusters using the "limit_bal" and "age" columns for the “customer_segments”:
```python
# Plot the clusters using the "limit_bal" and "age" columns
ccinfo_default_df.plot.scatter(
    x="limit_bal",
    y="age",
    c="customer_segments",
    colormap="winter")
```
![[credit-card-balance-age-scatter.png]]
- These groups are clearly segmented for “age,” however, we can observe a different result if we choose different features:
```python
# Plot the clusters using the "bill_amt" and "pay_amt" columns
ccinfo_default_df.plot.scatter(
    x="bill_amt",
    y="pay_amt",
    c="customer_segments",
    colormap="winter")
```
![[credit-card-bill-pay-scatter.png]]
- Since this dataset has eleven features, it is more challenging to segment the data. This does not necessarily indicate a problem with the K-means algorithm, but rather that there were too many factors that influenced the outcome to plot only two dimensions and get an accurate representation.
- Reducing the number of factors (dimensional reduction) comes at the expense of some accuracy. However, a reduced number of variables is much easier to visualize in a plot.
- Initialize the PCA module:
```python
# Import the PCA module
from sklearn.decomposition import PCA

# Instantiate the PCA instance and declare the number of PCA variables
pca = PCA(n_components=2)
```
- Each principal component will be a single column.
- Two components, `n_components=2`, are often used because this works well with a 2D visualization.
- Fit PCA model on the transformed credit card info DataFrame:
```python
# Fit the PCA model on the transformed credit card DataFrame
ccinfo_pca = pca.fit_transform(ccinfo_default_df)

# Review the first 5 rows of list data
ccinfo_pca[:5]
```
```text
array([[-11.4106317 ,  -1.19426208],
        [ -9.424725  ,  -0.75732157],
        [ -1.33620686,  -0.69534399],
        [  1.67884463,  -0.76676318],
        [ 21.58943237,  -0.9373152 ]])
```
- We can find out how much of that information each principal component contains by examining the explained variance of a principal component.
- **Explained variance** is the amount of variability in the data that can be attributed to each individual principal component. 
- We can measure the relative amount of information that one principal component contains compared to another by examining the proportion of explained variance.
- Calculate PCA explained variance ratio:
```python
# Calculate the PCA explained variance ratio
pca.explained_variance_ratio_
```
```text
array([0.95017303, 0.01898131])
```
- In general, the larger the variance explained by a principal component, the more important that component is for representing the data.
- Create DataFrame with transformed data:
```python
# Create the PCA DataFrame
ccinfo_pca_df = pd.DataFrame(
    ccinfo_pca,
    columns=["PCA1", "PCA2"]
)

# Review the PCA DataFrame
ccinfo_pca_df.head()
```
![[credit-card-pca-DataFrame.png]]
- Use elbow method to determine the best `k`:
```python
# Create a list to store inertia values and the values of k
inertia = []
k = list(range(1, 11))

# Append the value of the computed inertia from the `inertia_` attribute of the K-means model instance
for i in k:
    k_model = KMeans(n_clusters=i, random_state=1)
    k_model.fit(ccinfo_pca_df)
    inertia.append(k_model.inertia_)

# Define a DataFrame to hold the values for k and the corresponding inertia
elbow_data = {"k": k, "inertia": inertia}
df_elbow = pd.DataFrame(elbow_data)

# Review the DataFrame
df_elbow.head()

# Plot the elbow curve
df_elbow.plot.line(
    x="k",
    y="inertia"
)
```
![[credit-card-pca-elbow-curve.png]]
- Optimal value for `k` is 3.
- Determine the rate of decrease for each `k` value:
```python
# Determine the rate of decrease between each k value
k = df_elbow["k"]
inertia = df_elbow["inertia"]
for i in range(1, len(k)):
    percentage_decrease = (inertia[i-1] - inertia[i]) / inertia[i-1] * 100
    print(f"Percentage decrease from k={k[i-1]} to k={k[i]}:{percentage_decrease:.2f}%")
```
```text
Percentage decrease from k=1 to k=2: 67.75%
Percentage decrease from k=2 to k=3: 48.46%
Percentage decrease from k=3 to k=4: 34.36%
Percentage decrease from k=4 to k=5: 23.68%
Percentage decrease from k=5 to k=6: 27.19%
Percentage decrease from k=6 to k=7: 15.20%
Percentage decrease from k=7 to k=8: 13.88%
Percentage decrease from k=8 to k=9: 12.36%
Percentage decrease from k=9 to k=10: 5.96%
```
- Create K-means model with `k` = 3 on PCA data:
```python
# Define the model with 3 clusters
model = KMeans(n_clusters=3, random_state=0)

# Fit the model
model.fit(ccinfo_pca_df)

# Make predictions
k_3 = model.predict(ccinfo_pca_df)

# Create a copy of the PCA DataFrame
ccinfo_pca_predictions_df = ccinfo_pca_df.copy()

# Add a class column with the labels
ccinfo_pca_predictions_df["customer_segments"] = k_3

# Plot the clusters
ccinfo_pca_predictions_df.plot.scatter(
    x="PCA1",
    y="PCA2",
    c="customer_segments",
    colormap="winter"
    )
```
![[credit-card-pca-segmentation-scatter.png]]

---
>Related Notes: [[The Elbow Method]], [[Finding the Best k]]
>Tags: #AI #UL 
