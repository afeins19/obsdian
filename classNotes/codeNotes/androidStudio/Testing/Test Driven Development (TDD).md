The main principle of TDD: Write the test case **BEFORE** the implementation of the function (only for unit tests)

- Really try to make a single assertion per test case (We are testing ONE thing per test case)
- The idea is that if a test fails, we want to know immediately what caused it
# Work Flow
1. Write the function signature (what the function returns)
2. Write the test cases for that function 
3. Write the function logic so that it passes the tests
# What Makes a Good Test?
1. Scope - how much of our actual code is covered by our test case
2. Speed - how fast does our test case run 
3. Fidelity - how close are the test cases to an actual scenario (real world use)
# Flaky Tests
- tests that sometimes succeed and sometimes fail by external factors
- we really want to avoid writing these kinds of tests 
- usually happen when these test cases are dependent on other tests/factors 

# Equivalent classes
The Class of all inputs to the object we are testing which result in the correct functioning of the item we are testing. 

## Example (Equivalent Classes)
say you have the following registration form and want to test its functionality and validate the user input of this registration form. How many test cases should we write?
- we want want all of our test cases to cover the code
- we will take one test per one **equivalent class**

![[Pasted image 20231005204234.png]]

for this registration form, one equivalence class is all possible valid and non-taken usernames. If we have a test that checks for passing a valid username (i.e. peter1@gmail) then we dont have to check anything others from that equivalence class (i.e. joebob2@gmail, markzuck7@hotmail...) 

### Some Equivalence Classes for the example above...
#### Username Field
- testing Existing Username in Username field
- testing empty Username field
- testing invalid Username format 
- testing non-existant user 

#### Password Field
- testing incorrect password for a given user 
- testing empty password 

#### Confirm Password Field
- testing non-matching passwords between this and password field 
- testing empty field 
