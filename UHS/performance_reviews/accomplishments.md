# Portfolio of accomplishments 

## Dashboard/Report Automation
Successfully automated the following reports. These run without any (or with minimal) human intervention:

### FWIP Dashboard
My Role: Lead Developer

The FWIP dashboard was the first fully automated report in our department, setting a new standard for how operational data is delivered to leadership. It eliminated the need for manual compilation of follow-up metrics and replaced static Excel reporting with a dynamic, self-updating analytics tool. This initiative not only streamlined access to key performance data but also demonstrated the feasibility and value of full data pipeline automation within our team. Additionally, this dashboard allows us to have a more frequent reporting cadence in the future if we wish.

- **Total Time to Run Report**: 10 minutes 

- **Notable Features**:
	- **Organizational Impact:** Provided C-Suite executives, CBO managers, and team leads with daily, automated visibility into account follow-up activity
	- **Technical Achievement**: Designed and implemented a fully automated data pipeline using Python and SQL, handling data ingestion, cleaning, transformation, and visualization end-to-end
	- **Proof of Concept**: Our deparment's first foray into automation, which has since served as the model for many downstream reporting initiatives

### CBO Productivity & Quality Dashboard
Role: Lead Developer

Automated roughly 90% of the data for this dashboard. Tracks and calculates the productivity and quality scores for CBO employees and displays aggregate statistics. 
Will look to fully automate in the future allowing us to potentially refresh the data on a daily cadence. 
- **Time to run report**: 10-15 it minutes for manually processing excel file + 1 minute to run automated report 
- **Time Savings**: automated dashboard displays many different kinds of metrics based on collected data from CBO managers. Estimated time savings ~1-2 hours
- **Notable Features**:
	- productivity trending over time for teams and pools
	- automatically pulls the 2 most recent QR scores for each employee
	- displays time partitions of employee off time 
	- shows time adjustments per team as a percentage of total time
 
### Patient Access Processing and Dashboard (Experian)
Role: Lead Developer
Automated the ingestion and processing of an excel file pulled from Experian. 
Uses python to process and generate calculated columns as well as summary views on ingested data. Automatically commits data to our reporting database

### Report Users
- Patient Access Team
- Management
- Facility CFOs

#### Fully Automated the following Metrics
- Pre service collections
- Date of Service Collections
- Total PAS Collections

- **Total Time to Run Report**: 5 minutes
- **Time Savings**: roughly 2-3 hours 

### Futher Improvements
With the workflow that i developed here, i have built up a solid base of utility functions for processing data out of healthe and experian. 
This will speed up the process of creating more report automations like this in the future

	
### Rep Code Dashboard
Fully automated the trending of data on the performance of our 3rd party vendors in handling claims.
- **Time Savings**: query takes 35-45 minutes to run manually and compile into excel 

### Unposted Cash Report
A fully automated report that displays daily data about aggregated cash that has not been posted to an account yet. 
- **Time to Run Report**:  0 minutes
- **Notable Features**: 
	- automatically generates a PDF report for emailing 
	- displays daily data as opposed to weekly (previous)
	- Displays a trend over time of the signposted cash 

### MDC Report
Fully automated report on AR and credits data specifically for the Manatee diagnostic center.
**Time to run**: 0  minutes (fully automated)
**Noteable Features**:
- Utilized by Mark Cannon 

### Other Dashboard Projects/Enhancements
- Initial Denials
- Final denials
- Insurance Resequencing Dashboard
- Credits Dashboard
- CBO Dashboard

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
This will automate the collection of data for reports that require any form of manual entry from our end users 
such as the CBO Productivity Report and the FWIP report. Users of this site will be able to directly edit/create
entries or modify existing and historic entries. Once a change has been made, it may automatically trigger
a refresh with no manual intervention required.
- custom made website for creating manual report entry sachems and managing user permissions to edit reports.
- ChatGPT made a sick logo for it













