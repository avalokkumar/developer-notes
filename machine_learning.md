# Machine Learning A-Z


## The Machine Learning Process

1. Data Preprocessing
- Import the dataset
- Clean the dataset
- - Import the dataset
- - Handle missing data
- - Encode categorical data
- - Split the dataset into the Training set and Test set
- - Feature scaling

2. Modelling
- Build a model
- Train the model
- Test the model
- Make Predictions

3. Evaluation
- Calculate performance metrics
- - Confusion Matrix
- - Accuracy
- - Precision
- Make a verdict


## Splitting data into training set and test set

To split the data into training and test sets, we can use the `train_test_split` function from the `sklearn.model_selection` module. Here's an example:

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

In this process, we will split the dataset into two parts: the training set and the test set. The `test_size` parameter specifies the proportion of the dataset that should be included in the test set. In this case, we are using 20% of the data for testing. The `random_state` parameter is used to ensure that the data is split in the same way each time the code is run.

### Training Set
The training set is used to train the machine learning model. It contains a set of input features (X_train) and the corresponding target labels (y_train).
For example: 80% of the data is used for training the model.

* We use the training set to build the model and adjust its parameters to make accurate predictions. Then, we make a linear regression model that can predict the price of a house based on its size.

### Test Set
The test set is used to evaluate the performance of the trained model. It contains a set of input features (X_test) and the corresponding target labels (y_test).
For example: 20% of the data is used for testing the model.

* We use the test set to evaluate the model's performance on unseen data. This helps us understand how well the model generalizes to new data and whether it is overfitting or underfitting.

Equation: y = b0 + b1 * x1 + b2 * x2 + ... + bn * xn

> Note: Based on the comparison between the predicted value of y and the actual value of y, we can evaluate the performance of the model. We can use metrics such as the Mean Squared Error (MSE) or the R-squared value to assess the model's accuracy.

## Feature Scaling

Feature scaling is a technique used to standardize the range of independent variables or features of data. In data processing, it is also known as data normalization and is generally performed during the data preprocessing step.

Example:

```
X1          X2          X3          X4

1000        1           0.5         10
2000        2           1           20
3000        3           1.5         30
4000        4           2           40
....
,...
```

> Feature scaling always applies to the columns of the dataset, not the rows. It is important to apply feature scaling to ensure that all features contribute equally to the model training process and prevent any one feature from dominating the others.

### Types of Feature Scaling

1. Standardization (Z-score normalization)

Standardization scales the data to have a mean of 0 and a standard deviation of 1. It is calculated as follows:

```
X_std = (X - X_mean) / X_std_dev
```

* Its value lies between -3 and +3. Where X is the feature value, X_mean is the mean of the feature values, and X_std_dev is the standard deviation of the feature values.

> X_mean is the mean of the feature values, and X_std_dev is the standard deviation of the feature values. mean = sum(X) / n, std_dev = sqrt(sum((X - mean)^2) / n). Standard deviation is a measure of the amount of variation or dispersion of a set of values. Mean is the average of the values.


2. Normalization (Min-Max scaling)

Normalization scales the data to a fixed range, usually between 0 and 1. It is calculated as follows:

```
X_norm = (X - X_min) / (X_max - X_min)
```

* Its value lies between 0 and 1. Where X is the feature value, X_min is the minimum value of the feature, and X_max is the maximum value of the feature.

> X_min is the minimum value of the feature, and X_max is the maximum value of the feature. Min-Max scaling is used when the data does not follow a Gaussian distribution. It is sensitive to outliers in the data.


Lets consider a simple data set where we have annual income of different persons and age of different persons.

```
Annual Income (in $)    Age
50000                    25
60000                    30
67000                    32
70000                    39
80000                    25
90000                    35
```

The task here is to identify whether a person with lets say salary 60000 and age 30 is similar to which other person in the dataset. This is where we use clustering algorithms like K-means to group similar data points together.

> We can use feature scaling here to ensure that both the features (Annual Income and Age) contribute equally to the clustering process. If we don't scale the features, the model may give more weight to the feature with a larger range, which can affect the clustering results.

After applying Normalization, the data is scaled to a fixed range between 0 and 1. This ensures that both features contribute equally to the clustering process.

The value will look like:

Formula:
```
X_norm = (X - X_min) / (X_max - X_min)
```

Result:

```
Annual Income (in $)    Age
0.0                     0.0
0.2                     0.2
0.4                     0.3
0.5                     0.6
0.7                     0.0
1.0                     0.8
```


### Types of Variables in Data Set

1. **Categorical Variables**
- Nominal: No order (e.g., colors, countries)
- Ordinal: Order matters (e.g., low, medium, high)
- Binary: Two categories (e.g., yes/no, true/false)
- Dummy: Represent
- - 0: Absence of a category
- - 1: Presence of a category

2. **Numerical Variables**
- Discrete: Countable (e.g., number of cars)
- Continuous: Infinite values (e.g., height, weight)
- Interval: No true zero (e.g., temperature in Celsius)
- Ratio: True zero (e.g., weight, height)

3. **Text Variables**
- Unstructured data (e.g., reviews, comments)
- Requires text preprocessing (e.g., tokenization, stemming)

4. **Date/Time Variables**
- Time series data (e.g., stock prices, weather data)
- Extract features (e.g., day of the week, month)

5. **Mixed Variables**
- Combination of different types (e.g., address, name)
- Requires feature engineering (e.g., one-hot encoding, feature extraction)


### Independent and Dependent Variables

Sample Data:

**Data.csv**

```
Country          Age          Salary          Purchased 

France           44           72000           No
Spain            27           48000           Yes
Germany          30           54000           No
Spain            38           61000           No
Germany          40           63777.78        Yes
France           35           58000           Yes
Spain            38.77777778 52000           No
France           48           79000           Yes
Germany          50           83000           No
France           37           67000           Yes
```

1. **Independent Variables (Features)**
- Input variables
- Used to predict the dependent variable
- Denoted as X
- Example: In above example, Country, Age, and Salary are independent variables.




2. **Dependent Variable (Target)**
- Output variable
- Predicted by the independent variables
- Denoted as y
- Example: In above example, Purchased is the dependent variable. We want to predict whether a person will purchase a product based on the independent variables (Country, Age, Salary).


### Importing dataset
```py
dataset = pd.read_csv('Data.csv')
X = dataset.iloc[:, :-1].values # This will select all rows and all columns except the last one
y = dataset.iloc[:, -1].values # This will select all rows and the last column
```

## Handling Missing Data

Missing data is a common problem in real-world datasets. It can occur due to various reasons, such as data corruption, human error, or system failures. Handling missing data is an essential step in the data preprocessing pipeline to ensure the quality and reliability of the data.

### Strategies for Handling Missing Data

1. **Remove Rows with Missing Data**
- Pros: Simple and straightforward
- Cons: May lose valuable information

2. **Impute Missing Data**
- Pros: Retains valuable information
- Cons: May introduce bias or inaccuracies

3. **Use Advanced Techniques**
- Pros: Handles missing data more effectively
- Cons: Requires more computational resources

### Techniques for Imputing Missing Data

1. **Mean/Median Imputation**
- Replace missing values with the mean or median of the column
- Suitable for continuous numerical data

> Example:
    
```py
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(strategy='mean')
X[:, 1:] = imputer.fit_transform(X[:, 1:])
```


2. **Mode Imputation**
- Replace missing values with the mode (most frequent value) of the column
- Suitable for categorical data

> Example:
    
```py
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(strategy='most_frequent')
X[:, 0] = imputer.fit_transform(X[:, 0])
```

3. **K-Nearest Neighbors (KNN) Imputation**
- Replace missing values with the average of the K-nearest neighbors
- Suitable for both numerical and categorical data

> Example: 
        
```py
from sklearn.impute import KNNImputer

imputer = KNNImputer(n_neighbors=2)
X = imputer.fit_transform(X)
```

4. **Multiple Imputation**
- Generate multiple imputed datasets and combine the results
- Suitable for complex datasets with missing data

> Example:
        
```py
from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer

imputer = IterativeImputer(max_iter=10, random_state=0)
X = imputer.fit_transform(X)
```

5. **Predictive Imputation**
- Use machine learning models to predict missing values
- Suitable for datasets with complex relationships

> Example:
        
```py
from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer

imputer = IterativeImputer(max_iter=10, random_state=0)
X = imputer.fit_transform(X)
```


## Encoding Categorical Data Step 1

Categorical data refers to data that represents categories or groups. It can take on a limited number of values and is often represented as text or labels. Machine learning models require numerical input, so we need to encode categorical data into a numerical format.

Example:

```
Country          Age          Salary          Purchased

France           44           72000           No
Spain            27           48000           Yes
Germany          30           54000           No
Spain            38           61000           No
Germany          40           63777.78        Yes
France           35           58000           Yes
Spain            38.77777778 52000           No
France           48           79000           Yes
```

In above example, Country and Purchased are categorical variables. We need to encode these variables into numerical format before using them in a machine learning model.
The country names (France, Spain, Germany) are nominal categorical variables and to use it in a machine learning model, we need to encode them into numerical format.
THe way to encode these variables is to use One-Hot Encoding.

### One-Hot Encoding

One-Hot Encoding is a technique used to convert categorical data into a numerical format. It creates binary columns for each category and assigns a 1 or 0 to indicate the presence of a category.

```py
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder
```

Example:

```
Country_France    Country_Spain    Country_Germany    Purchased

1                 0                0                  0
0                 1                0                  1
0                 0                1                  0
0                 1                0                  0
0                 0                1                  1
1                 0                0                  1
0                 1                0                  0
1                 0                0                  1
```

## Encoding Categorical Data Step 2

After applying One-Hot Encoding to the categorical variables, we need to handle the issue of multicollinearity. Multicollinearity occurs when two or more independent variables are highly correlated, leading to redundancy in the data.

### Encoding Independent Variables

To avoid multicollinearity, we need to drop one of the binary columns created by One-Hot Encoding. This is known as the dummy variable trap.

```py
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder

ct = ColumnTransformer(transformers=[('encoder', OneHotEncoder(), [0])], remainder='passthrough')
X = np.array(ct.fit_transform(X))
```

Output:
    
```
    Country_Spain    Country_Germany    Country_France        Age    Salary     Purchased
    
    1.0                0.0                  0.0                    44     72000      No
    0.0                0.0                  1.0                    27     48000      Yes
    0.0                1.0                  0.0                    30     54000      No
    0.0                0.0                  1.0                    38     61000      No
    0.0                1.0                  0.0                    40     63777.78   Yes
    1.0                0.0                  0.0                    35     58000      Yes
    0.0                0.0                  1.0                    38.77777778 52000 No
    1.0                0.0                  0.0                    48     79000      Yes
    0.0                1.0                  0.0                    50     83000      No
    1.0                0.0                  0.0                    37     67000      Yes
```

### Encoding Dependent Variables

For the dependent variable, we can use Label Encoding to convert categorical labels into numerical format.

```py
from sklearn.preprocessing import LabelEncoder

le = LabelEncoder()
y = le.fit_transform(y)
```

Output:
    
```
    0
    1
    0
    0
    1
    1
    0
    1
    0
    1
```


Excercise:

titanic.csv

```
PassengerId,Survived,Pclass,Name,Sex,Age,SibSp,Parch,Ticket,Fare,Cabin,Embarked
2,1,1,"Cumings, Mrs. John Bradley (Florence Briggs Thayer)",female,38.0,1,0,PC 17599,71.2833,C85,C
4,1,1,"Futrelle, Mrs. Jacques Heath (Lily May Peel)",female,35.0,1,0,113803,53.1,C123,S
7,0,1,"McCarthy, Mr. Timothy J",male,54.0,0,0,17463,51.8625,E46,S
11,1,3,"Sandstrom, Miss. Marguerite Rut",female,4.0,1,1,PP 9549,16.7,G6,S
12,1,1,"Bonnell, Miss. Elizabeth",female,58.0,0,0,113783,26.55,C103,S
22,1,2,"Beesley, Mr. Lawrence",male,34.0,0,0,248698,13.0,D56,S
24,1,1,"Sloper, Mr. William Thompson",male,28.0,0,0,113788,35.5,A6,S
28,0,1,"Fortune, Mr. Charles Alexander",male,19.0,3,2,19950,263.0,C23 C25 C27,S
53,1,1,"Harper, Mrs. Henry Sleeper (Myna Haxtun)",female,49.0,1,0,PC 17572,76.7292,D33,C
55,0,1,"Ostby, Mr. Engelhart Cornelius",male,65.0,0,1,113509,61.9792,B30,C
```


```py
# Importing the necessary libraries
import numpy as np
import pandas as pd

from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder, LabelEncoder

# Load the dataset
dataset = pd.read_csv('titanic.csv')


# Identify the categorical data
categorical_features = ['Sex', 'Embarked', 'Pclass']
# categorical_indices = [dataset.columns.get_loc(col) for col in categorical_columns]


# Implement an instance of the ColumnTransformer class
ct = ColumnTransformer(
    transformers=[
        ('encoder', OneHotEncoder(), categorical_features)
    ],
    remainder='passthrough'
)


# Apply the fit_transform method on the instance of ColumnTransformer
X = ct.fit_transform(dataset)


# Convert the output into a NumPy array
X = np.array(X)


# Use LabelEncoder to encode binary categorical data

le = LabelEncoder()
y = le.fit_transform(dataset['Survived'])


# Print the updated matrix of features and the dependent variable vector

print("Updated matrix of features: \n", X)
print("Updated dependent variable vector: \n", y)
```

