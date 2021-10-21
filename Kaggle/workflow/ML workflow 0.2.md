# Table of content:
1. [Define problem](#1-define-problem)
2. [Gather data](#2-gather-data)
3. [Initial exploration of data](#3-initial-exploration-of-data)
4. [Pre-processdata](#4-pre-processdata)
    1. [Data clean-up](#1-data-clean-up)
    2. [Data imoutation](#2-data-imputation)
    3. [Encode categorical features](#3-encode-categorical-data)
5. [Data analyze](#5-data-analyze)
    1. Visualization
    2. Variance
    3. Correlation
    4. Feature importance
6. [Feature selection](#6-feature-selection)    
    1. Based on "Data analyze"
7. [Feature engineering](#7-feature-engineering)
8. [Train-val-test split](#8-train-val-test-split)
9. [Prepare data](#9-prepare-data)
    1. Transform data
    2. Feature scaling
    3. Check for imbalance
10. [Train some models](#10-train-some-models)
11. [Evaluate models](#11-evaluate-models)
12. [Tune selected models](#12-tune-selected-models)
13. [Production](#13-production)

# 1. Define problem
# 2. Gather data
## Import libaries
```
import os
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```
## Load data
```
path_to_data = "../data/original/"
file_names = os.listdir(path_to_data)
df = pd.read_csv(path_to_data+file_names[0])
```
# 3. Initial exploration of data
## First look
```
df.info()
```
## Numerical interpretation
```
df.describe()
```
## Categorical interpretation
```
pd.pivot_table(train, index='OriginalTweet', columns='Sentiment', values='Location', aggfunc='count')
```
# 4. Pre-processdata
##    1. Data clean up
### 1. Handle duplicates and unrellevant features
##    2. Data imoutation
###        1. Handle missing values
##    3. Encode categorical features
# 5. Data analyze
##    1. Visualization
##    2. Variance
##    3. Correlation
##    4. Feature importance
# 6. Feature selection    
##    1. Based on "Data analyze"
# 7. Feature engineering
# 8. Train-val-test split
# 9. Prepare data
##    1. Transform data
##    2. Feature scaling
##    3. Check for imbalance
# 10. Train some models
# 11. Evaluate models
# 12. Tune selected models
# 13. Production
Retrain selected model on whole dataset
