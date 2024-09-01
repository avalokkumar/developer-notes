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


## Splitting the dataset into the Training set and Test set

To evaluate the performance of a machine learning model, we need to split the dataset into two parts: the training set and the test set. The training set is used to train the model, while the test set is used to evaluate its performance on unseen data.


Q. Do we need to apply feature scaling before splitting the dataset into the training set and test set or after splitting the dataset?

A. It is recommended to apply feature scaling after splitting the dataset into the training set and test set. This is because feature scaling should be done on the training set only to prevent data leakage from the test set. If feature scaling is applied before splitting the dataset, information from the test set may leak into the training set, leading to biased results.


```py
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
```

Excercise:

```py
# Import necessary libraries
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
import pandas as pd

# Load the Iris dataset
data = pd.read_csv('iris.csv')

# Separate features and target
X = data.iloc[:, :-1]
Y = data.iloc[:, -1]

# Split the dataset into an 80-20 training-test set
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.2, random_state=42)

# Apply feature scaling on the training and test sets
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train) # scaler.fit_transform is used for training set. it will learn the parameters from the training set.
X_test = scaler.transform(X_test)

# Print the scaled training and test sets
print(X_train)
print(X_test)
```

## Feature Scaling

Feature scaling is a technique used to standardize the range of independent variables or features of data. In data processing, it is also known as data normalization and is generally performed during the data preprocessing step.

### Why do we need Feature Scaling?

1. **Machine Learning Algorithms**
- Many machine learning algorithms use Euclidean distance to make predictions.
- Features with larger scales may dominate the distance calculation.
- Feature scaling ensures that all features contribute equally to the model.

2. **Convergence Speed**
- Gradient descent converges faster on scaled features.
- It reduces the number of iterations required to reach the minimum.

3. **Regularization**
- Regularization techniques like Lasso and Ridge are sensitive to feature scales.
- Feature scaling helps in regularization by penalizing large coefficients.

4. **Distance-Based Algorithms**
- Distance-based algorithms like K-Nearest Neighbors (KNN) are sensitive to feature scales.
- Feature scaling ensures that the algorithm is not biased towards features with larger scales.

### Types of Feature Scaling

1. **Standardization (Z-score normalization)**
- Scales the data to have a mean of 0 and a standard deviation of 1.
- Suitable for algorithms that assume normally distributed data.
- Equation: `z = (x - mean) / std_dev`
- - mean is the mean of the data.
- - std_dev is the standard deviation of the data. It is calculated as the square root of the variance which is the average of the squared differences from the mean.
- Its value will be in the range of +3 and -3
- It works well when the data follows a Gaussian distribution. It is not sensitive to outliers in the data.

2. **Normalization (Min-Max scaling)**
- Scales the data to a fixed range, usually between 0 and 1.
- Suitable for algorithms that require data to be on the same scale.
- Equation: `x_norm = (x - min) / (max - min)`
- - min is the minimum value of the data.
- - max is the maximum value of the data.
- It always result in the range of 0 to 1
- It is recommended to use Min-Max scaling when the data follows a Gaussian distribution. It is sensitive to outliers in the data which means that it can be affected by outliers in the data. Outliers are data points that are significantly different from other data points in the dataset.

3. **Robust Scaling**
- Scales the data based on the interquartile range (IQR).
- Suitable for datasets with outliers.
- Equation: `x_robust = (x - Q1) / (Q3 - Q1)`
- - Q1 is the first quartile (25th percentile).
- - Q3 is the third quartile (75th percentile).


4. **MaxAbs Scaling**
- Scales the data based on the maximum absolute value.
- Suitable for sparse datasets.
- Equation: `x_maxabs = x / max(abs(x))`
- - max(abs(x)) is the maximum absolute value of the data.

5. **Quantile Transformation**
- Maps the data to a uniform or normal distribution.
- Suitable for non-Gaussian data.
- Equation: `x_quantile = F(x)`
- - F(x) is the cumulative distribution function of the data.


Example:

```py
from sklearn.preprocessing import StandardScaler

sc = StandardScaler()
X_train[:, 3:] = sc.fit_transform(X_train[:, 3:]) # Apply feature scaling to the training set. It will scale the columns from 3 to the end.
X_test[:, 3:] = sc.transform(X_test[:, 3:]) # Apply feature scaling to the test set. It will scale the columns from 3 to the end.
```

Note:
We are performing `fit_transform` on the training set and `transform` on the test set. This is because we want to scale the test set based on the parameters learned from the training set. This ensures that the scaling is consistent across both sets. If we were to use `fit_transform` on the test set, it would learn new parameters and the scaling would be different from the training set.


#### Excercise:

> Coding exercise: Feature scaling for Machine Learning

```py
# Import necessary libraries
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

# Load the Wine Quality Red dataset
# dataset = pd.read_csv('wineqality-red.csv', sep=';')
dataset = pd.read_csv('winequality-red.csv', delimiter=';')

# Separate features and target
X = dataset.iloc[:, :-1]
y = dataset.iloc[:, -1]

# Split the dataset into an 80-20 training-test set
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Create an instance of the StandardScaler class
scaler = StandardScaler()

# Fit the StandardScaler on the features from the training set and transform it
X_train = scaler.fit_transform(X_train)

# Apply the transform to the test set
X_test = scaler.transform(X_test)

# Print the scaled training and test datasets
print(X_train)
print(X_test)
```

## Regressions
<img width="652" alt="image" src="https://github.com/user-attachments/assets/72114b95-a17f-4124-9925-38842b75d338">


Regression is a fundamental concept in statistics and machine learning, used to model and analyze relationships between variables. The primary goal of regression is to predict the value of a dependent variable (often called the "target" or "outcome") based on one or more independent variables (also known as "predictors" or "features"). Regression models are particularly useful when the dependent variable is continuous, like predicting house prices, stock prices, or temperatures.

### Key Concepts in Regression
* Dependent Variable: The outcome or the variable you are trying to predict. It's also known as the response variable.
* Independent Variables: The predictors or features that are used to predict the dependent variable.
* Regression Line: A line that best fits the data points in a regression model. In simple linear regression, it is represented as y=mx+b, where m is the slope, and b is the y-intercept.
* Residuals: The differences between observed and predicted values. Residuals are used to assess the accuracy of the regression model.

---

### 1. Simple Linear Regression

<img width="305" alt="image" src="https://github.com/user-attachments/assets/a3756d73-a8ce-4b9d-856a-e3c31bb9633b">

- One independent variable
- Linear relationship between variables
- Equation: `y = b0 + b1 * x1`
- - y is the dependent variable
- - x1 is the independent variable
- - b0 is the y-intercept
- - b1 is the slope of the line

#### Ordinary Least Squares (OLS) Method
- Minimizes the sum of squared differences between observed and predicted values
- Finds the best-fitting line that minimizes the sum of squared residuals

```py
from sklearn.linear_model import LinearRegression

dataset = pd.read_csv('Data.csv')
X = dataset.iloc[:, :-1].values
y = dataset.iloc[:, -1].values

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

regressor = LinearRegression()
regressor.fit(X_train, y_train)
```

> Formula for OLS
```
b1 = sum((x - x_mean) * (y - y_mean)) / sum((x - x_mean)^2)
b0 = y_mean - b1 * x_mean
```

y = b0 + b1 * x1 where b0 is the y-intercept and b1 is the slope of the line.

---

### 2. Multiple Linear Regression

<img width="531" alt="image" src="https://github.com/user-attachments/assets/ff3e497b-dde3-406e-a45a-fdef12085932">


Multiple Linear Regression is a statistical method used to understand the relationship between one dependent variable (the outcome you want to predict) and two or more independent variables (the predictors or factors that influence the outcome). It’s like extending simple linear regression, which deals with just one predictor, to handle multiple predictors.

#### Key Concepts of Multiple Linear Regression

1. **Dependent Variable (Target/Outcome)**: This is the variable you want to predict or explain. For example, predicting house prices.
   
2. **Independent Variables (Predictors/Features)**: These are the variables that are used to predict the dependent variable. For example, predicting house prices based on the size of the house, number of bedrooms, location, etc.

3. **Equation**: The relationship can be represented with a linear equation:

   \[
   y = b_0 + b_1x_1 + b_2x_2 + \ldots + b_nx_n + \epsilon
   \]

   - \( y \): Dependent variable (e.g., house price)
   - \( x_1, x_2, \ldots, x_n \): Independent variables (e.g., size, bedrooms, location)
   - \( b_0 \): Intercept (the value of \( y \) when all \( x \)'s are zero)
   - \( b_1, b_2, \ldots, b_n \): Coefficients (they show how much \( y \) changes with a change in each \( x \))
   - \( \epsilon \): Error term (captures the variation in \( y \) not explained by the predictors)

4. **Objective**: The goal is to find the best-fitting line (or plane, or hyperplane) that minimizes the difference between the predicted values and the actual values of the dependent variable. This is done by adjusting the coefficients (\( b_1, b_2, \ldots, b_n \)).

#### How It Works

1. **Fit the Model**: The model is trained on a dataset by finding the best coefficients that minimize the difference between the predicted values and actual values. This is usually done using a method called **Least Squares** which minimizes the sum of squared errors.

2. **Prediction**: Once the coefficients are determined, you can use the model to make predictions on new data by plugging the values of independent variables into the equation.

#### Example

Suppose you want to predict the price of a house based on its size (in square feet), the number of bedrooms, and the distance to the city center.

#### Data Example

| Size (sq ft) | Bedrooms | Distance to City Center (miles) | House Price ($) |
|--------------|----------|---------------------------------|-----------------|
| 2000         | 3        | 5                               | 300,000         |
| 1600         | 2        | 3                               | 250,000         |
| 2400         | 4        | 8                               | 350,000         |
| 3000         | 4        | 6                               | 400,000         |

#### Building the Model

1. **Define the variables**:
   - Dependent variable: House Price (\( y \))
   - Independent variables: Size (\( x_1 \)), Bedrooms (\( x_2 \)), Distance to City Center (\( x_3 \))

2. **Formulate the equation**:
   
   \[
   \text{House Price} = b_0 + b_1 \times \text{Size} + b_2 \times \text{Bedrooms} + b_3 \times \text{Distance to City Center}
   \]

3. **Training the Model**:
   - Using the given data, the model learns the coefficients (\( b_0, b_1, b_2, b_3 \)) that best predict the house prices.

4. **Making Predictions**:
   - For a house that is 2200 sq ft, with 3 bedrooms, and 4 miles from the city center, plug in the values into the equation:

   \[
   \text{Predicted Price} = b_0 + b_1 \times 2200 + b_2 \times 3 + b_3 \times 4
   \]

### Assumptions of Multiple Linear Regression

1. **Linearity**: The relationship between dependent and independent variables is linear.
2. **Independence**: The observations are independent of each other.
3. **Homoscedasticity**: The variance of residual errors is constant across all levels of the independent variables.
4. **Normality**: The residuals (errors) of the model should be normally distributed.
5. **No Multicollinearity**: The independent variables should not be too highly correlated with each other.

### Advantages and Limitations

- **Advantages**:
  - Easy to understand and implement.
  - Works well when the relationship is linear and the assumptions are met.
  - Can handle multiple predictors.

- **Limitations**:
  - Not suitable for non-linear relationships.
  - Performance can be affected if the assumptions are violated.
  - Sensitive to outliers which can skew the results.


#### Assumptions of linear regression

1. **Linearity**(Linear relationship between Y and each X): The relationship between the independent and dependent variables is linear.
    - The relationship between the independent and dependent variables can be represented by a straight line.
    - It can be checked using a scatter plot of the data.

2. **Homoscedasticity**(Equal Variance): The variance of the residuals is constant.
    - The residuals are equally spread across all values of the independent variables.
    - The residuals are not dependent on the independent variables.
    - It can be checked using a scatter plot of the residuals.

3. **MultiVariate Normality**(Normality of error distribution): The residuals are normally distributed.
    - The residuals are normally distributed.
    - The residuals have a mean of zero.
    - The residuals are independent of each other.
    - It can be checked using a Q-Q plot or a histogram of the residuals.

4. **Independence**(of observations. includes "no autocorrelation"): The residuals are independent of each other.
    - The residuals are independent of each other.
    - There is no correlation between the residuals.
    - It is important to check for autocorrelation in time series data.
    - It can be checked using a scatter plot of the residuals.

5. **Lack of Multicollienarity**(Predictors are not correlated with each other): The independent variables are not highly correlated with each other.
    - The independent variables are not highly correlated with each other.
    - Multicollinearity can lead to unstable coefficients and inaccurate predictions.
    - It can be checked using a correlation matrix or a variance inflation factor (VIF).

6. **The outlier check**: The presence of outliers can significantly affect the regression model.
    - Outliers are data points that are significantly different from other data points in the dataset.
    - Outliers can affect the regression coefficients and the model's accuracy.
    - It can be checked using box plots or scatter plots of the data.

---

### 3. Polynomial Regression

- Non-linear relationship between variables
- Equation: `y = b0 + b1 * x1 + b2 * x1^2 + ... + bn * x1^n`


