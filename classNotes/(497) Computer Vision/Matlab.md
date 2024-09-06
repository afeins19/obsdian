# Example: Solar Panel Energy Generation (Theoretical vs Actual)

### Constants 
```python
lat = 42 + 17/60
declenation_june_21 = 23.45
```

### Converting to radians manually & with a matlab function
```python 
lat = lat*pi/180

dec = deg2rad(dec) # converting to radians 
```

### Creating vectors 
in this example, we're creating a vector to represent time in 15 minute increments (25% of an hour) until 8pm (20).
```python 
t = 5.5:0.25:20
```

#### Output 
```
t =

  Columns 1 through 3

    5.5000    5.7500    6.0000

  Columns 4 through 6

    6.2500    6.5000    6.7500

  Columns 7 through 9

    7.0000    7.2500    7.5000

  Columns 10 through 12

    7.7500    8.0000    8.2500

  Columns 13 through 15

    8.5000    8.7500    9.0000

  Columns 16 through 18

    9.2500    9.5000    9.7500

  Columns 19 through 21

   10.0000   10.2500   10.5000

  Columns 22 through 24

   10.7500   11.0000   11.2500

  Columns 25 through 27

   11.5000   11.7500   12.0000

  Columns 28 through 30

   12.2500   12.5000   12.7500

  Columns 31 through 33

   13.0000   13.2500   13.5000

  Columns 34 through 36

   13.7500   14.0000   14.2500

  Columns 37 through 39

   14.5000   14.7500   15.0000

  Columns 40 through 42

   15.2500   15.5000   15.7500

  Columns 43 through 45

   16.0000   16.2500   16.5000

  Columns 46 through 48

   16.7500   17.0000   17.2500

  Columns 49 through 51

   17.5000   17.7500   18.0000

  Columns 52 through 54

   18.2500   18.5000   18.7500

  Columns 55 through 57

   19.0000   19.2500   19.5000

  Columns 58 through 59

   19.7500   20.0000

```

### Applying a shift on vectors
```python
LST = t - 1 + 14.6/60
```

### Using a Formula 
```python
sunangle = sin(dec) * sin(lat) + cos(dec) * cosd(15*)LST-12)); 
```
- `cosd()` accepts its argument in degrees 
- semicolon means the output wont be displayed 

# Plotting 
```python 
plot(t,sunangle) # creates a plot 
```

# Creating Scripts 
you can scroll through your command inputs in the history and create a script for it.
1. select all code (portions that you want)
2. click 'create live script'

# Comments & Sections 
sections are discretely runable sections of code 
```
% comments are written using percent signs 

%% Sections are denoted with 2 percent signs 
```

# Indexing Vectors
say we have a vector of 10 elements 
```
y = 1:10 
```
we can get the element at the 5th position (index) with `y(5)` *note that MATLAB start indexing at 1*

# If Statements 
```
userIn = input('y/n')

if userIn == 'y'
	disp('cool')
elseif userIn == 'n'
	disp('uncool')
else 
	disp('wut?')
end 
```
n
