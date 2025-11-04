# Structure
1. name and goal of project (my role in this project: tech lead, manager, etc.)
2. what did this project achieve (time savings, new features, etc.)
3. End users of this project

# Portfolio of accomplishments 

## Dashboard/Report Automation
Successfully automated the following reports. These run without any (or with minimal) human intervention:

### FWIP Dashboard
Project lead on this dashboard. Fully automated report used by C-Suite management, executives, and CBO managers.  Shows statistics as well as raw data about how the billing teams are working through their pools of accounts that are past follow up date
- **Total Time to Run Report**: 10 minutes 
- **Time savings**: unknown as this report was built from the ground up to be automated but would likely take 1-2 hours to manually report out all of the metrics captured
- **Notable Features**:
	- intuitive graphics that allow users to quickly understand team performance
	- ability to quickly drill into specific accounts that should be prioritized

### CBO Productivity & Quality Dashboard
Automated roughly 90% of the data for this dashboard. Tracks and calculates the productivity and quality scores for CBO employees and displays aggregate statistics
- **Time to run report**: 10-15 it minutes for manually processing excel file + 1 minute to run automated report
- **Time Savings**: automated dashboard displays many different kinds of metrics based on collected data from CBO managers. Estimated time savings ~1-2 hours
- **Notable Features**:
	- productivity trending over time for teams and pools
	- automatically pulls the 2 most recent QR scores for each employee
	- displays time partitions of employee off time 
	- shows time adjustments per team as a percentage of total time 
### Patient Access Processing and Dashboard (Experian)
Automated the ingestion and processing of an excel file pulled from Experian. Uses python to process and generate calculated columns as well as summary views on ingested data. Automatically commits data to our reporting database

### Report Users
- Patient Access Team

#### Fully Automated the following Metrics
- Pre service collections
- Date of Service Collections
- Total PAS Collections

- **Total Time to Run Report**: 5 minutes
- **Time Savings**: roughly 2-3 hours 

### Futher Improvements
with the workflow that i developed here, i have built up a solid base of utility functions for processing data out of healthe and experian. this will speed up the process of creating more report automations like this in the future


	

### Rep Code Dashboard
Fully automated the trending of data on the performance of our 3rd party vendors in handling claims.
- **Time Savings**: query takes 35-45 minutes to run manually and compile into excel 

### Unposted Cash Report
fully automated report that displays daily data about aggregated cash that has not been posted to an account yet. 
- **Time to Run Report**:  0 minutes
- **Notable Features**: 
	- automatically generates a PDF report for emailing 
	- displays daily data as opposed to weekly (previous)
	- Displays a trend over time of the signposted cash 

### MDC Report
Fully automated report on AR and credits data specifically for the Manatee diagnostic center.
**Time to run**: 0  minutes (fully automated)
**Noteable Features**:
- Utilized by the department director himself

# Current Initiatives

### RCM Data Architecture Initiative
working to apply modern db/software engineering practices to create a platform for building our data pipelines. This includes 
- Integrating modern tools such as
	- Airflow
	- DBT
	- git/github
	- python 
- designing DIM and FACT tables for our reporting areas
- using the new tables and STAR schema to create data marts to serve our reports

### Purpose 
our current reporting workflow is inefficient and relies on excel sheets, various existing reports, and unstructured data. By applying the tools/ideas mentioned above, we will be able to:
- greatly increase the speed at which dashboards are created
- fully automate the data loading process to our reports
- Be able to back-fill and change report granularity with ease
- join reports that populate at different time frames/cadences

### Manual Data Entry Reporting Platform 
(tentative name RADAR) - Revenue-cycle Analytics Data-entry And Reporting platform 
- custom made website for creating manual report entry sachems and managing user permissions to edit reports.

# Goals
- I want to learn deeper about our business so i can better forsee and tailor the reports for our end users to make them more productive












