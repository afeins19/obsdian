the performance of a machine learning model depends on:
- hyperparameters 
- processing different types of variables to the model 

# Categorial Data Encoding 
data of type 'string' or 'category' are finite in number. In general there are 2 types of categorical data.
- **Ordinal** - inherent order to the data (position in a race)
- **Nominal** - data does not have inherent order (gender)

## Ordinal Encoding 
the encoding of ordinal categorical data into integers in the order of sequence. This can be done with ***skelarn.preprocessing.LabelEncoder*** 
- encode the target labels with a value between 0 and (n-1) classes 

# One Hot Encoding 
a vector of size n where n=number of categories being encoded. Each unique categorical element is given a unique vector of size n. **sklearn.preprocessing.OneHotEncoder***
- note that OneHotEncoder needs shaped data 

### Drawbacks 
- not effective with a large number of levels
- not effective with a large number of categorical features in the dataset 

# Binary Encoding 
a combination of hash encoding and one-hot encoding. Binary encoding usually works really well when there are a high number of categories 

# Target Encoding 
a technique for assigning a numerical value to each category based on the relationship between the category and the target variable. Simplly representing categorical data with some representative number such as the average of some attributes. This is typically used for callssification tasks

