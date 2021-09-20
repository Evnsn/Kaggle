# Table of content
0. [Buisness and data understanding](https://github.com/Evnsn/Kaggle/blob/main/Kaggle/workflow/README.md#0-buisness-and-data-understanding)
1. [Import data and libaries](https://github.com/Evnsn/Kaggle/blob/main/Kaggle/workflow/README.md#1-import-data-and-libaries)
   - Data integration and formatting
2. [Exploratory data analysis](https://github.com/Evnsn/Kaggle/blob/main/Kaggle/workflow/README.md#2-exploratory-data-analysis)
   - Data cleaning
3. [Train, val & test split](https://github.com/Evnsn/Kaggle/blob/main/Kaggle/workflow/README.md#3-train-val--test-split)
4. [Preprocessing](https://github.com/Evnsn/Kaggle/blob/main/Kaggle/workflow/README.md#4-preprocessing)
   - Transform data - Numerical (Feature selection)
   - Transform data - Categorical
   - Feature selection
5. [Pick some models](https://github.com/Evnsn/Kaggle/blob/main/Kaggle/workflow/README.md#5-pick-some-models)
6. [Select model](https://github.com/Evnsn/Kaggle/blob/main/Kaggle/workflow/README.md#6-select-model)
7. [Fintune model](https://github.com/Evnsn/Kaggle/blob/main/Kaggle/workflow/README.md#7-fintune-model)
8. [Pick best model and retrain on all the data](https://github.com/Evnsn/Kaggle/blob/main/Kaggle/workflow/README.md#8-pick-best-model-and-retrain-on-all-the-data)


# 0. Buisness and data understanding
Download the data and make it available in your enviroment


# 1. Import data and libaries
## Some basic libaries
```
import numpy as np
import pandas as pd

import matplotlib.pyplot as plt
import seaborn as sns
```
### Usfull functions/methodes:
```
pd.read_csv('data.csv', sep=',')
```

## Data integrating and formatting
### Usfull functions/methodes:
```
df['column'] = np.nan                     # Fills a (new) column with placeholders.
df.drop('column', inplace=True, axis=1)   # Removes column
pd.concat([...])
pd.merge()
```

# 2. Exploratory data analysis
## Data cleaning
### Handle missing data
#### Types:
- **MCAR (Missing completly at random):** 
  - % of missingness is compleatly random
  - **Solution:** Safe to delete rows (can replace as well)
- **MAR (Missing at random):** 
  - % of missingness other variabels, but not itself.
  - **Solution:** Safe to delete rows (can replace as well)
- **NMAR/MNAR (Not missing at random):**  
  - % of missingness dependent on itself.
  - **Solution:** Not safe to delete rows, can produce bias. Try to replace.
#### How to resolve missing data ([Link](https://towardsdatascience.com/how-to-handle-missing-data-8646b18db0d4)):
- Delete the rows with missing data (MCAR).
- Mean, median & mod.
  - Mean => Distribution symetric.
  - Median => Distribution skeweed or great outliers.
  - Mod => Distribution skeweed or categorical.
- Generate (predict): Make a model to predict the missing variable based on the other variables (regression, KNN, etc).  
  
Road map: [Handle missing data](https://miro.medium.com/max/875/1*_RA3mCS30Pr0vUxbp25Yxw.png)  
#### Usfull functions/methodes:
```
df[df['column'] == 0] = np.nan # Replace 0 with NA so we can compute the correct mean, medain and mod.
df['column'].fillna(df['column'].mean())
```

### Handle duplicates
...

### Remove outliers
...

### Handle multicollinearity
Multicollinearity occurse when independent variabels are correlated. This will potetial makes the model sensetive to small changes and weakness the statistical power of the  model. Models who are effected are; Linear Regression, Logistic Regression, KNN, and Naive Bayes algorithms.
We can determen the degree of collinearity with VIF. 
#### Two types:
- Structural multicollinearity: This is the result of feature engineering (it's created).
- Data multicollinearity: This type of multicollinearity is present in the data itself (not created).
#### Variance Inflation Factors ([VIF](https://statisticsbyjim.com/regression/multicollinearity-in-regression-analysis/)):
- 1 indicates that there is no correlation.
- 1-5 indicates that there is a moderate correlation.
- 5< indicates that there is a critical correlation
#### Do you have to solve multicollinearity?
- Moderate multicollinearity, you may not need to resolve it.
- Multicollinearity does not influence the predictions, precision of the predictions, and the goodness-of-fit statistics. If your primary goal is to make predictions, and you not understand understanding the features, you don’t need to reduce severe multicollinearity.
#### How to solve multicollinearity:
- Remove some of the highly correlated independent variables.
- Linearly combine the independent variables.
- Perform an analysis designed for highly correlated variables, such as principal components analysis or partial least squares regression.
- Ridge or Lasso regression solves this problem. 
#### Usfull functions/methods:
```
from statsmodels.stats.outliers_influence import variance_inflation_factor
vif_data["feature"] = X.columns
vif_data["VIF"] = [variance_inflation_factor(X.values, i) for i in range(len(X.columns))]
```
### Remove noise
- Regression
### Handle inconsistent data
...


# 3. Train, val & test split
It is important that we split the data before we pre-processes it. We should base our data transformation on the training set to avoid a bias model.
### Usfull functions/methodes:
```
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, random_state=42)
```


# 4. Preprocessing
## Transform data - Numerical (Feature scaling)
Feature scaling is essential for algorithms whcih is based on distance (KNN, Regression, SVM, MLP etc). Algorithm that not use distance calculation does not require scaling (Naive Bayes, Tree based)  
Feature scaling may squeez preformance, and is equally important as hyperparameter tuning.
### Nested transfomations?
Choose one.
### Different transformation for different features?
It is okey to have different transformation for different features (I think).
### Main methodes:
- **Normalization** [0, 1]:  
  When you do not know the distribution of your data or when you know the distribution is not Gaussian (a bell curve).  
  Is usfull for algorithms that does **NOT** make assuption about the distribution of the data.
  - KNN
  - ANN
- **Standarization** (mean=0, std=1):  
  Assumes that your data has a Gaussian distribution, but this does not strictly have to be true.
  Is usfull for algorithms that make assuption about the distribution of the data.
  - Linear regression
  - Logistic regression
  - LDA
  - PCA
### Some other methodes:
- Log Transform: Used to normalize skeweed data.
- Max-abs scaling
- Min-max scaling
- Power transformer
- Quantile transformer normal
- Quantile transformer uniform
- Robust scaling
- Standard scaling

## Transform data - Categorical:
- One-hot-encoding
- Label-encoding
- Binarize


# 5. Pick some models
![ML algo map](https://scikit-learn.org/stable/_static/ml_map.png)
## Regression
- Linear Regression
- Lasso Regression
- Ridge Regression
- Polynomial Regression
- Robust Regression — RANSAC (?)
- Gaussian process regression
- Support Vector Regression
- Decision tree
- Random Forest
- Boosted Trees
- Neural Network
## Classification
- Support Vector Classifier
- Random Forest
- Logistic Regression
- Boosted Tree
- Neural networks


# 6. Select model


# 7. Fintune model


# 8. Pick best model and retrain on all the data 
