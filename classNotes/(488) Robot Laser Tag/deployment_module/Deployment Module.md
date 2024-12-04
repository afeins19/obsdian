CMPSC488 Section 2
Github: https://github.com/joeoakes/CMPSC488FA24Sec2Team2
Testing Status Page (Spreadsheet):
https://docs.google.com/spreadsheets/d/1gX3ksFSNGmzlHVL34X6IZp0Qe264xLXucDIeHmrW3fk/edit?usp=sharing
# Testing Environment and Framework
We employ the use of Pytest to run our unit, integration, and hardware tests. Tests
are written for all Python modules and are setup in the following way:
### Directory Structure
*the `__init__.py` tells python to treat all files in this directory as python packages allowing us to import into our test modules*.

```
├── src/ # main source code
│ ├── module1.py
| ├── module2.py
| ├── __init__.py
|
├── tests/ # tests folder
│ ├── test_module1.py
│ ├── test_module2.py
| ├── __init__.py
|
├── requirements.txt
├── README.md```

```

### Example Unit Test

```python
def test_detect_object_success(mock_torch_hub, mock_model):
	"""Test detect_object with a successful detection."""
	model_path = "../src/yolo/model"
	weights_path = "../src/yolo/weights"
	image_path = "../Dataset/images"
	result = detect_object(model_path, weights_path, image_path)
	
	assert result == (100, 50, 200, 150, "MockedObject")
	mock_torch_hub.assert_called_once_with(model_path, weights_path,
	source="local")
	mock_model.return_value.assert_called_once_with(image_path)
```


this is an example unit test for evaluating the performance of the YOLO module that's used in object recognition. The parameters in the function signature are 
special pytest objects called fixtures that are used to create common objects to
be tested in the function below. These are marked with `@pytest.fixture`
decorators. The function above runs tests on a torch hub and model that are fixtures generated to perform this test among others.

# Continuous Integration
The uniform and centralized testing directory structure makes it simple to run tests. Locally, this can be done by running pytest tests (tests being the name of the directory that holds all our tests) in the parent directory of the project. This is done automatically when commits are made to main through Github Actions using a YAML script.

### YAML Test Script
(link:https://github.com/joeoakes/CMPSC488FA24Sec2Team2/actions/runs/12002110016/job/33453581141)

Test Status Page
(link: https://docs.google.com/spreadsheets/d/1gX3ksFSNGmzlHVL34X6IZp0Qe264xLXucDIeHmrW3fk/edit?usp=sharing)


1. installs the correct version of python
2. downloads all dependencies (or pulls from cache)
3. runs pytest on the parent directory (triggering all tests)
4. returns the test results and cleans up.

Our Testing Status Page Features the names of each test function, a brief
description of the test case, the creator of the test and its status (as well as some
comments).

# Test Statistics

Using SQL, these side data displays automatically display some general statistics
about our testing status, namely:
- Total number of working, pending, and not working tests
- Number of failures in each testing category (only shows categories with at least one failure)

### Test Log 
 ![[Pasted image 20241203210659.png]]
### Statistics
![[Pasted image 20241203210828.png]]