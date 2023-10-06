# Testing In Android
- test cases obviously test if our code is working
- there are many different kinds of tests

# Test Types

![[Pasted image 20231005200020 1.png]]

# Unit Tests
- most granular test cases (ex. checking the output of individual functions in the code like sum() or average())
- only tests within specific functions of our app (doesnt depend on any other frameworks besides main programming language)
- should make up roughly 70% of the test cases 

# Integration Tests 
- tests how different components of our app work together (Fragment and ViewModel)
- Think testing interaction 
- Rely on android framework to run (requires some emulator or device
- should make up roughly 20% of tests 

# UI Tests
- tests that check if many or all components of your app work together well and if the UI looks like it should 