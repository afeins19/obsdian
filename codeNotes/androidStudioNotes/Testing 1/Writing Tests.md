
# Test Witing location
app/src/androidTest/com/example/<app_name>/
- right click and create a new **kotlin class** file (this class represents test for a single **activity**)

# Writing the Test 
1. Boiler Plate: (replace names with activity you're testing)
	1. @run(...) above class decleration
	2. @get:Rule above val activityRule =...
	3. @test above test function
	4. @After above tearDown Function

2. @Test Section - decorates testing functions
	1. each function represents a specific item to test
	2. onView(withId(com.example.frugl_app.R.id.loginn).perform(click()))
	3. Intents.intennded(hasComponent(Login::class.java.name)) - only include this if the action you are testing a function that takes you to a **new activity**...the example above is clicking the login button on the main activity so we need to see if that takes you to the login activity which is seperate from the mainactivity
3. 