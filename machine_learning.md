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

