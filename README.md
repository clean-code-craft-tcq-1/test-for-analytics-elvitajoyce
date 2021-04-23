# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Read/write access of the data
3. Threshold should be defined
4. PDF report generator dependency
5. Notification utility dependency
6. Date and time library dependency

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No 			| We need not test the pdf converter as it is a third party utility
Counting the breaches       | Yes			| This is part of the software being developed. We should test if the number of breaches reported is as expected
Detecting trends            | Yes			| This is part of the software being developed. We should test if the number of trends reported is as expected 
Notification utility        | Yes			| This is part of the software being developed. We should test if the notification is sent once the new report is available

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write the count of breaches to the pdf when the data crosses the threshold
4. Write number of trends with date and time to the PDF when the data is continuously increasing for 30mins
5. Write "Server not found" to PDF when the server is not reachable
6. Write "New report generated" when there is a new PDF report is available. 

(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | csv data	  | Notification success/failure| Fake the actual notifying utility
Report inaccessible server | csv file 	  | server not found error		| Fake the server store
Find minimum and maximum   | csv data 	  | min and max data     		| None - it's a pure function
Detect trend               | csv data	  | Trends with date and time   | Mock increase of data for 30mins
Write to PDF               | csv data	  | pdf data               		| Fake PDF utility 
