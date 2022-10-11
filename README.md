# Machine learning: diamonds price

The goal of project is to implement a supervised machine learning model to estimate the price of a set of diamond with a specific features.

### **EDA**

No nulls in training dataset, some columns are numerical type and others one are categorical. But a few records have value 0 in columns x, y, z.

For categorical features cut, color and clarity is applied a method to encode. They are relevant in diamonds quality.

Categorical column  city is removed, its not significant in diamonds quality.

Volume is a new column created with existing features x, y, z which are removed.

Get stats and correlation matrix. Carat and volume has high correlation with price.

Test dataset have same behavior as train dataset. No null values, few records with value 0 in same features, numerical and categorical.

Applying same methods to encode and create new feature, you can see similar stats and correlation.

In addition, at the end of process, stats of price prediction are similar than stats of price training.

---

### **WorkFlow**

- Encoding

    Apply categorical features clarity, color, cut, city.

    In this case, it's a manual ordinal number because the higher or lower value affect to estimate the price.
    
    Encoding with an automatic method, such as OrdinalEncoder, you can't control to assign a high value to a high choice. It's studied every feature to know the quality order.

    Checked that it's important to improve model metric.

- Add feature

    Volume is a new feature created with existing features x, y, z. In one column there is same information that in three columns.
    
    Features x, y and z are removed.

    Volume has very high correlation with carat, could drop that feature. But it's checked that model metric doesn't improve (it's worst).
    
- Scaling

    Scaling all features with RobustScaler, StandardScaler, MinMaxScaler and applying log function.

    RobustScaler is selected. RMSE result is very similar.

---

### **Best model**

Model selected is HistGradientBoostingRegressor. 

Training with several models and comparing their metric results.

- LinearRegression
- RandomForestRegressor
- GradientBoostingRegressor
- HistGradientBoostingRegressor

- Cross validation

    Applying cross validation, get results of RMSE in several splits of dataset and calculate mean of all splits for every model.
    
    Estimators RandomForest and Boosting have best results. Particularly, HistGradientBoosting, is better model when dataset has more than 10.000 samples.

- Hyperparams

    For HistGradientBoostingRegressor model, it's used GridSearchCV to get best value of depth and iterations.
    
        max_depth=8
        max_iter=1000

HistGradientBoostingRegressor model has the best result of RMSE and better execution time.

This model is the best in first and second position.

The difference between first and second position is the encoding in categorical features and no include volume (neither remove x, y, z).

    cut: No change.
         
         'Fair' = 1,
         'Good' = 2, 
         'Very Good' = 3, 
         'Premium' = 4, 
         'Ideal' = 5

    color: First position in order asdending, D is 1 and J is 7. Second position in order descending, D is 7 and J is 1.
           
           'D' = 1,
           'E' = 2,
           'F' = 3,
           'G' = 4,
           'H' = 5,
           'I' = 6,
           'J' = 7

    clarity: Values in first position are opposite than values in second position.
    
            Frist position:
             'VVS1' = 1,
             'VVS2' = 2,
             'VS1' = 3,
             'VS2' = 4,
             'SI1' = 5,
             'SI2' = 6,
             'I1' = 7,
             'IF' = 8

            Second position:
             'I1' = 1,
             'SI2' = 2,
             'SI1' = 3,
             'VS2' = 4,
             'VS1' = 5,
             'VVS2' = 6,
             'VVS1' = 7,
             'IF' = 8

---

### **Analysis**

The key points:

- Encoding

    It's very important to improve the metrics. Assign a manual value for every feature and every value in order of quality known.

- Features

    New volume feature has improved the results.

    Why a new feature with very high correlation with other feature (carat) improves the results?
    why other fetures do not affect as they should? The 4C's are the main properties in a diamond. In this orden: cut, color, clarity and carat. Correlation data in dataset don't show this relation and model doesn't give importance to the most important properties (cut).
    TODO: Try most weight to cut.

- Scaling

    RobustScaler is selected. 

- Model

    Improve model with hyperparams values.

---

### **Folder structure**

Datasets aren't included.

```
└── project
    ├── .gitignore
    ├── README.md
    └── notebooks
```
