the input data quality heavily influences a machine learning models performance 
- the model may learn from incorrect data without proper cleaning leading to inaccurate predictions or classifications 
- data transformation
- feature selection
- normalization
- reduction 

### Data Cleaning 
the process of identifying and correcting errors in the dataset 
- dealing with missing data or inconsistencies 
- removing duplicates
- handling outliers 

### Handling missing data 
happens in errors with collection
- **inputation**
	- replace missing values with substituted values such as the mean median or mode 
	- more sophisticated models include regression imputation 
- **deletion** 
	- remove the instance with missing values from the dataset 
	- easy but we lose that data

### Removing Duplicates 
- might skew the model by biasing the data with multiple duplicate entries 

### Outlier Detection 
outliers are data points that significantly deviate from the other observations in the data set 
- dealt with using statistical methods such as Z-score 
- mll models such as clustering or anomaly detection algorithms

### Data Scaling 
a technique used to standardize the range of independent variables or features of data 
- prevents any feature from dominating the others
- sometimes it helps to make the algorithm learn better or faster 
- **Min-Max Normalization**
	- normalizing scales the data to a fixed range (usually 0 or 1)
- standardization 
	- scales the data to a distribution with a mean of 0 and a standard deviation of 1 

### Encoding Categorical Variables 
the process of encoding categorical data to numerical values (we do this because the input type to ml models is always numerical under the hood)

- **One-hot Encoding**
	- create new binary columns for each category/label in the original columns 

# Data Splitting 
a technique to divide the data set into two or three sets. We may...
- typically split the data into training, validation, and test sets
- training set will train the model
- validation set will tune the models parameters
- test set provides an unbiased evaluation of the final model 
- this technique prevents over-fitting of our model to some particular subset of data 

# Handling Missing Values 
techniques for handling missing values include
- deletion: removing the rows with missing values 
- imputation: replacing the missing values with statistical measures like mean, median, mode etc.

![[Screen Shot 2024-01-29 at 1.55.02 PM.png]]

# Feature Selection 
the process of selecting features in your data that contribute most to the prediction variable or output in which you are interested 
- relevant features in your data can decrease the accuracy of many models 
- particularly important with high-dimensional data 

### Benefits of feature selection
- reduce overfitting
- improving accuracy
- reducing training time 

# Tools & Libraries 
- **Pandas (python)**
	- provides a wide range of functionalities for data cleaning, including handling missing  values, removing duplicates and standardizing data 
- **DataHeroes (python)**
	- uses **coresets to reduce the size of the dataset to a smaller subset** that maintains the statistical properties and corner cases of the full dataset -> same performance 

# Pandas 

## Series 
pandas data structure - **Series**
- a seriese is a one-dimensional array like object containing a sequence of values 
![[Screen Shot 2024-01-29 at 2.07.55 PM.png]]

## DataFrame 
a rectangular table of data 
- an ordered collection of columns 
- a default one consisting of the integers [0, (n-1)]
![[Screen Shot 2024-01-29 at 2.08.53 PM.png]]

assgining indecies and column names to data is really easy in pandas dataframes 

![[Screen Shot 2024-01-29 at 2.10.06 PM.png]]


## Handling missing data 