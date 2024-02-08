# Source Sets & Directories 
Integrated Unit Tests: androidTest directory
JUnit and Unit Tests: test directory
![[Pasted image 20231005211720.png]]
# Build.gradle (Module:app) - Depedencies
![[Pasted image 20231005211555.png]]

- we can add libraries to our gradle with any the following
- when these libraries are inserted in to Build.gradle and sync is run, they will be added into their respective directories the implementation/testImplementation/andriodTestImplementation is the specifier for that 
``` 
implementation 'testLibrary' 
testImplementation 'testLibrary' 
androidTestImplementation 'testLibrary'
```

# Writing a Singleton Unit(basic function test) 
- create this in a kotlin object file
- inside the file containing your main activity 
# Example
![[Screen Shot 2023-10-06 at 1.07.33 PM.png]]

# Writing Test Cases
- right click on the kotlin object file we just created then go -> generate -> Test 
- Select (test) folder as this is a basic unit test 