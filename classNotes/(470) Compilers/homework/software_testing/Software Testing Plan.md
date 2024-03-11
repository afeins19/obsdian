# Test Plan for Student Grader 

Aaron Feinberg 
CMPSC-470-002

---

## 1. Introduction

This Test Plan describes our plan for testing the Course Grading Software. This software helps calculate and display grades for high school students and includes features for managing student information and showing grades in different chart formats.

## 2. Test Items

We will test the following parts of the software:

- **Student Class:** We'll check if the software correctly handles student numbers, names, and grades. This includes testing all the basic functions like adding and changing student details.
- **Test Grade Input Method:** We’ll make sure the software accurately records each student's test grades.
- **Histogram Display Method:** The software should correctly show test scores as histograms (bar charts).
- **Final Grade Calculation Method:** We need to test if the software correctly averages all test scores to give a final grade.
- **Grading Class Methods:** This includes checking if the software can correctly save and load student data, sort and show results, and display grades as pie charts.

## 3. Software Risk Issues

Possible problems include:

- Mistakes in calculating grades.
- Losing data when saving or loading files.
- Charts (like histograms and pie charts) showing incorrect information.

## 4. Features to be Tested

We will focus on testing:

- How well the software checks and handles the information entered for students.
- The accuracy of calculations for grades.
- The correctness and clarity of the charts showing grades.
- How well the software handles saving, loading, and organizing student data.

## 5. Features Not to be Tested

We won't test:

- How the software performs under very heavy use.
- How it works in a networked setup.

## 6. Approach

Our testing will include:

- **Unit Testing:** Looking at each part of the software on its own to make sure it works right.
- **Integration Testing:** Checking how different parts of the software work together.
- **User Interface Testing:** Making sure that the menus and screens are easy to use and work as expected.

## 7. Item Pass/Fail Criteria

A part of the software passes the test if it:

- Works without crashing or causing errors.
- Does its job correctly.
- Handles wrong inputs or unusual situations without problems.

## 8. Suspension Criteria and Resumption Requirements

We'll stop testing if:

- We find a big problem that affects many parts of the software.
- The software doesn't work as expected in more than half of our tests.

We'll start testing again when:

- The big problems are fixed.
- We've updated and approved our test plans based on these fixes.

## 9. Test Deliverables

We expect to produce:

- A detailed list of test scenarios.
- Automated test scripts where possible.
- Reports summarizing our findings from the tests.

## 10. Testing Tasks

Key tasks are:

- Creating and writing down test scenarios.
- Running tests manually and using automated scripts.
- Keeping track of any problems we find.
- Making sure problems are fixed and retesting to confirm.

## 11. Environmental Needs

We need:

- Computers with either Windows 10 or Linux.
- The required software and tools for testing.
- Sample data for thorough testing.

## 12. Responsibilities

- The Quality Assurance (QA) team will handle the testing and reporting.
- The development team will work on fixing any issues found during testing.

## 13. Staffing and Training Needs

- Our current team should be enough for the planned tests.
- We’ll provide training on the software and testing tools.

## 14. Schedule

### 14.1 Planning and Setup

- **Duration:** 1 week
- **What We'll Do:** Set up the testing area, get the tools ready, and finalize the testing plan.
- **Goals:** A ready testing environment and an approved plan.

### 14.2 Test Case Development

- **Duration:** 2 weeks
- **What We'll Do:** Create detailed test scenarios and review them to make sure we’ve covered everything.
- **Goals:** A complete set of test scenarios ready to use.

# **15. Risks and Contingencies**

Risks include delays in bug fixes. Contingency plans involve allocating additional resources if necessary.

# **16. Approvals**

This plan requires approval from the Project Manager and the Head of Quality Assurance.