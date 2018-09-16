#Handover

##Test Scenarios
Number | Test Case Name
------------ | -------------
1 | Super Policy with Non-UHG Requirement - UW Flow
2 | Super Policy with Non-UHG Requirement - NB Flow
3 | Super Policy with Non-UHG Requirement - UW Update Flow
4 | LOA and Corro - UW Flow
5 | LOA and Corro(BGB) - UW Flow
6 | LOA and Corro(BGB) - NB Flow
7 | NPW Policy Level - NB Flow
8 | UHG End to End - UW Flow
9 | Submit Requirements - API
10 | Create Policy - API
11 | Create Policy - STP - API
12 | Retrieve Requirements - API
13 | Create Tele Interview - API

### Explanation
* Detailed Step 
* Step : Search Life & Search Policy
* Step : If there are any Outstanding Action then withdraw
* Dependency
* UW Checker


##Script

### Dev Script 
  * For Debugging propose  TAL-EWF-Debug.jmx
  * Messy, include everything, deprecated scripts
  
### Stg Script TAL-EWF-UI.jmx TAL-EWF-API.jmx TAL-EWF-DataCreation.jmx
  * For Test Sanity test before formal test, Data Creation propose
  * Removed deprecated script, useless scrit depends on the Environment at that time

### Prod Script  TAL-EWF-LG.jmx
  * For Run Test in LG
  * Change Configuration to LG variable e.g. Test Data Path, Test Result Path, Driver Path, Proxy Setting 
  
##Test Data Preparation

### For All UI Scenarioa(1-8) 
TAL-EWF-DataCreateion.jmx / CreatePolicy-API
Change Loop to 1.5 Times totol work loads 
e.g 1 Hour Peak Load Test, Total UI work
Number | Work Load / Hr
------------ | -------------
1 | 32
2 | 32
3 | 6
4 | 4
5 | 4
6 | 4
7 | 2
8 | 38
Total | 122
1.5X| 183

Record Application RefNo e.g. PTS01001 - PTS01183
Leave "40" applications for sanity test each scenarios "3-5" Loops
  e.g. PTS01001 - PTS01040 (Taken for Sanity)
The Rest of them for Peak Loat Test
  e.g. PTS01041 - PTS01183

Plan for seperate application RefNo for different UI Scenarios
  e.g Scenario1: PTS01041 - PTS01073 
  e.g Scenario2: PTS01074 - PTS01106
  e.g Scenario3: PTS01107 - PTS01013

Modify All CSV files in /TestData to identical with what you planned. 

### For  2: Super Policy with Non-UHG Requirement - NB Flow
Issue: Dependency with Scenario 1
In TAL-EWF-DataCreation.jmx
Step1 : Change Loop Number in Test Group : 1_Super Policy with Non-UHG Requirement
Step2 : Change RefNo in TestData/pre_Super Policy with Non-UHG Requirement.csv to meet what you planned in previous step. e.g Scenario2: PTS01074 - PTS01106 
Step3 : Run Test Group : 1_Super Policy with Non-UHG Requirement - UW Flow in TAL-EWF-DataCreation.jmx

In TAL-EWF-UI.jmx
Step4 : Double Check Loops number and RefNo in 2_Super Policy with Non-UHG Requirement - NB Flow.csv have setup properly

### For  3: Super Policy with Non-UHG Requirement - UW Update Flow
Issue: Application will not consumed, can always use one application to update life details
At the moment, PTS00130 is the application for this scenario.
Note: Before execution, make sure the firstname is not Performance0, otherwise the response time of first sampler will be too short.

### For  6: LOA and Corro(BGB) - NB Flow
Issue: Dependency with Scenario 5
In TAL-EWF-DataCreation.jmx
Step1 : Change Loop Number in Test Group : 5_LOA and Corro(BGB) - UW Flow
Step2 : Change RefNo in TestData/pre_LOA and Corro(BGB) - UW Flow.csv to meet what you planned in previous step.
  e.g Scenario6: PTS01101 - PTS01106 
Step3 : Run Test Group : 5_LOA and Corro(BGB) - UW Flow in TAL-EWF-DataCreation.jmx

In TAL-EWF-UI.jmx
Step4 : Double Check Loops number and RefNo in 6: LOA and Corro(BGB) - NB Flow.csv have setup properly


TO-DO!!
### For  9: Submit Requirements - API
  Step1: Create Application e.g. PTS001 with Create Poilcy API
  Step2: UW Manager Login search and click Initial Assessment on the Life in PTS001
  Step3: Click Add Requirement button
  Step4: Change Sub category to Non-UHG
  Step5: Select All of requirements(Usually 10 requirements), Click Next, Click submit
  Step6: Copy and Paste All of the Requirement ID to Test Data File
  
  Tips: 10 Requirment ID for 1 Hour Test in 75/Hr workload
  
### For  10: Create Policy - API
  Make Sure test data for previous test have been removed in TestData/10_CreatePolicy.csv
  
  Tips: 10 Requirment ID for 1 Hour Test in 75/Hr workload

### For  11: Create Policy - STP - API

### For  12: Retrieve Requirements - API

### For  13: Create Tele Interview - API

## Payload Parameterization Explanation


## Test Exectution
### Sanity Test
### Test Data Preparation
### Test Script Configuration : TAL-EWF-LG.jmx
  * Path in LG
### Migrate Package to LG
  * Lastest TAL-EWF-LG.jmx
  * TestData folder
  

##Monitoring
###Integration - Azure App Insights
###PAS DB - DBA

