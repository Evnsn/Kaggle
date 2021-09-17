# Table of content
0. Buisness and data understanding
1. Import data and libaries
   - Data integration and formatting
2. Exploratory data analysis
   - Data cleaning
3. Train, val & test split
4. Preprocessing
   - Data transformating
5. [Pick some models](https://github.com/Evnsn/Kaggle/blob/main/Kaggle/workflow/README.md#5-pick-some-models)
6. Select model
7. Fintune model
8. Pick best model and retrain on all the data 

# 0. Buisness and data understanding
## Download the data and make it available in your enviroment

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
#### Solution:
...

### Handle duplicates
...

### Remove outliers
...

### Handle multicollinearity
Multicollinearity occurse when independent variabels are correlated. Vi kan determen the degree of collinearity with VIF.
#### Two types:
- Structural multicollinearity: This is the result of feature engineering (it's created).
- Data multicollinearity: This type of multicollinearity is present in the data itself (not created).
#### Variance Inflation Factors ([VIF](https://statisticsbyjim.com/regression/multicollinearity-in-regression-analysis/)):
- 1 indicates that there is no correlation.
- 1-5 indicates that there is a moderate correlation.
- 5< indicates that there is a critical correlation
#### How to solve multicollinearity:
- Remove some of the highly correlated independent variables.
- Use Ridge or Lasso regression 


### Remove noise
- Regression

### Handle inconsistent data
...

# 3. Train, val & test split
### Usfull functions/methodes:
```
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, random_state=42)
```
# 4. Preprocessing
## Data transformating

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