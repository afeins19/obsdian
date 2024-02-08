# Contents
- Regression 
- How to otain lline of est fit
- Multiple Linear Regression
- Python tools and libraries 

# Regression 
	a statisical tool for the investigation of relationships between variables. 
- finding the relationship between dependent and independent variables 
### Regression Analysis
	a form of predictive modeling which investigates the relationship etween a dependent (target) and independent variable(s). independent variables are also known as predictors. 
- indicates the strength of impact of multiple independent variables on a dependent variables 
### Simple Linear Regression
- measures how strong the relationship is between 2 variables 
- uses a straight line (of best fit) to model the relationship 

### Nonlinear regression models 
- representing the relationship with a curved line 
	Example:$$Y = a +bx + cx^2$$
### Examples of Linear Regression 
- predicting house prices 
	- given some dataset of bedroom numbers, square footage, location, etc. 
- stock price prediction
	- using historical stock data, predict the future price of a stock 
- employee performance prediction 
	- given data on employee characteristics, predict their future job performance or productivity 

# Linear Regression Model
$$Y = a + bX$$
- X = independent variablle
- Y = dependent variable

where...
- a - constant which equals the value of Y when X=0
- X - independent variable that is predicting Y 
- Y - value of dependent variable that is being predicted 
- b - slope of regression line u.e. how much y changes for each one unit change in X

### Line of Best Fit
	a straight line that best represents the data on a scatter plot 
- best linear approximation for some set of data 
![[Screen Shot 2024-01-17 at 2.04.50 PM.png]]

### How to obtain best fit value
	we define some function to represent the error between our prediction and the actual data. We then minimize this error function. Its common to use the ordinary least square method. 

![[Screen Shot 2024-01-17 at 2.06.28 PM.png]]

### Finding the value of Beta_0 

![[Screen Shot 2024-01-17 at 2.08.46 PM.png]]
- note that this value depends on some average values from the data set 
### Finding Beta_1
![[Screen Shot 2024-01-17 at 2.10.50 PM.png]]
- in the bottom part, we  meaningfully represent this information to be useful for our model 
- note that the sum((x1-x_hat)(y-y_hat)) is the covariance between x and y 
- we then normalize this value to x (dividing by sum of squares of x)
- putting it together, we divide the covariance of x and y by the covariance of just x 

# R-Squared (goodness of fit)
	a numebr that indicates how well data fits a statistical model 
- defined between [0,1] 
- higher value indicates a better fit 

equation: 1 - ((sum of squares between y actual and y predicted)/(sum of squares between actual y values and their mean))