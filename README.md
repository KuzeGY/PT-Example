# TAL-EWF-PT Handover - Greyson
 
## Test Scenarios
Scenario Number | Test Case Name
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

### Detailed ExplaTest Step Details compared based on Test Strategy
* Scenario 1 : Super Policy with Non-UHG Requirement - UW Flow
	 * Test Step : Add 3 Non-UHG Requirements : Click Add Requirements, Change Sub-category to Non-UHG, Select Three Requirements, Click Submit
  * Test Step : Complete It : Click Action - Click Complete - Click Submit, Iterate 3 times
* Step : Search Life & Search Policy
  * Test Step : Search Application Ref No : Select category to "Life" or "Policy", Click Life or Policy Start with "L-" or "P-"
* Step : If there are any Outstanding Action then withdraw
  * So far All of applications created by create poilcy do not have Outhstanding Action
* UW Checker : UWmanger do not have Authority Level and Varsha Kudav cannot use in UAT, All of UW flow have added additional UW Checker Step in the Script.

## Script 

### TAL_EWF_API.jmx
  * Script Include all API scenarios.
  * Usually run in local machine for scripting, debugging 

### TAL_EWF_UI.jmx 
  * Script Include all UI scenarios.
  * Usually run in local machine for scripting, debugging 
  
### TAL-EWF_DataCreation.jmx
  * For creating test data before formal test.

### TAL-EWF_Sanity.jmx
  * For Run Sanity Test to check environment status.

### TAL-EWF_LG.jmx
  * For Run formal test in Load Generator Machine.
  * Configuration changed to LG variable e.g. Test Data Path, Test Result Path, Driver Path, Proxy Setting , Throughput
  
## Test Data Preparation

### Create PEGA Application For All UI Scenarioa(1-8) 
TAL-EWF-DataCreateion.jmx / CreatePolicy-API
Change Loop to 1.5 Times totol work loads 
e.g 1 Hour Peak Load Test, Total UI work

Scenario Number|Work Load / Hr
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

* Step1 : Record Application RefNo e.g. PTS01001 - PTS01183
	* Leave "40" applications for sanity test each scenarios "3-5" Loops e.g. PTS01001 - PTS01040 (Taken for Sanity)
	* The Rest of them for Peak Loat Test e.g. PTS01041 - PTS01183

* Step2 : Modify TestData/10_CreatePolicy.csv to keep RefNo identical to Step1

* Step3 : Run CreatePolicy Test Group

* Step4 : Plan for seperate application RefNo for different Test Scenarios
  	* e.g Scenario1: PTS01041 - PTS01073 
  	* e.g Scenario2: PTS01074 - PTS01106
  	* e.g Scenario3: PTS01107 - PTS01013

* Step5 : Modify All CSV files in TestData to identical with what you planned in Step 4. 

### For  2: Super Policy with Non-UHG Requirement - NB Flow
Issue: Dependency with Scenario 1
In TAL-EWF-DataCreation.jmx
* Step1 : Change Loop Number in Test Group : 1_Super Policy with Non-UHG Requirement Senario:2
* Step2 : Change RefNo in TestData/1_Super Policy with Non-UHG Requirement.csv to meet what you planned in previous step. e.g Scenario2: PTS01074 - PTS01106 
* Step3 : Run Test Group : 1_Super Policy with Non-UHG Requirement - UW Flow in TAL-EWF-DataCreation.jmx
* Step4 : Double Check TestData/2_Super Policy with Non-UHG Requirement - NB Flow.csv setup properly

### For  3: Super Policy with Non-UHG Requirement - UW Update Flow
Issue: Application will not consumed, can always use one application to update life details
At the moment, PTS00130 is the application for this scenario.
Note: Before execution, make sure the firstname is not Performance0, otherwise the response time of first sampler will be too short.

### For  6: LOA and Corro(BGB) - NB Flow
Issue: Dependency with Scenario 5
In TAL-EWF-DataCreation.jmx
* Step1 : Change Loop Number in Test Group : 5_LOA and Corro(BGB) - UW Flow to meet how many workload designed for run Senario:6
* Step2 : Change RefNo in TestData/5_Super Policy with Non-UHG Requirement.csv to meet what you planned in previous step. 
* Step3 : Run Test Group : 5_LOA and Corro(BGB) - UW Flow in TAL-EWF-DataCreation.jmx
* Step4 : Double Check TestData/6_Super Policy with Non-UHG Requirement - NB Flow.csv setup properly

### For  9: Submit Requirements - API
* Step1: Create Application e.g. PTS001 with Create Poilcy API
* Step2: UW Manager Login search and click Initial Assessment on the Life in PTS001
* Step3: Click Add Requirement button
* Step4: Change Sub category to Non-UHG
* Step5: Select All of requirements(Usually 10 requirements), Click Next, Click Submit
* Step6: Copy and Paste All of the Requirement ID to TestData/9_Submit Requirements - API.csv e.g. 3000381 - 3000390
  
  Note: 10 Requirment ID for 1 Hour Test in 75/Hr workload
  
### For  10: Create Policy - API
	Make Sure tested data for previous test have been removed in TestData/10_CreatePolicy.csv

### For  11: Create Policy - STP - API
	Make Sure tested data for previous test have been removed in TestData/11_CreatePolicy-STP.csv

### For  12: Retrieve Requirements - API
	All of PolicyID for Retrieve Requirement is 1765010, No need for change.
	
### For  13: Create Tele Interview - API
	Make Sure tested data for previous test have been removed in TestData/13_Create Tele Interview - API.csv

## CreatePolicy, CreatePolicy-STP, Create TI Payload Parameterization Explanation
* <Id> ${AppID} </Id> Incremental e.g. 341bba42-0e9d-434f-a2ee-3553f8500001,341bba42-0e9d-434f-a2ee-3553f8500002,...
* <RefNo> ${RefNo} </RefNo> Incremental e.g. PTS00001, PTS00002,...
* <BirthDate> ${DOB} </BirthDate> Incremental e.g. 1960-01-01, 1960-01-02,...
	* To avoid EB Check but have risk on IB error like Invalid Premium Sum number
* <Id>${QuoteID}</Id> Incremental e.g. 95224332-5a6f-4c4d-84ef-2778fed00001,95224332-5a6f-4c4d-84ef-2778fed00002,...
* <Id>${PolicyID}</Id> Incremental e.g. c31edde9-ac56-4120-a96e-5439e4700001,c31edde9-ac56-4120-a96e-5439e4700002,...
* <Id>${LifeID}</Id> Incremental e.g. d024fdcf-96d3-465e-b13f-e157ac400001,d024fdcf-96d3-465e-b13f-e157ac400002,...

## Test Exectution
### 0.Manual Sanity Test
	Test Open Blocker scenarios, Test recently fixed scenario
	
### 1.Automation Sanity Test
* In TAL_EWF_Sanity.jmx, Each UI scenario run TWO iterations, Each API scenario run Three Requests in Three minutes. 
* Prepare and double check test data for Sanity Test set properly in "TestData" folder.
* Run All of Test group in TAL_EWF_Sanity.jmx.

### 1.Peak Load Test (Local)
* Prepare and double check test data for Peak Load Test set properly in "TestData" folder.
* Run All of Test group in TAL_EWF_UI.jmx and TAL_EWF_API.jmx.

### 2.Peak Load Test (LG)
* WinSCP LG IP : 10.134.17.65 User: gyang Password: Yh900916
	* Check There is no changes in TAL_EWF_UI.jmx
	* Check All latest *.csv file have migrated in TestData folder
	
* Putty LG IP : 10.134.17.65 User: gyang Password: Yh900916
	* cd TestScript
	* jmeter -n -y -f TAL_EWF_LG.jmx -l LinuxLG-log.jtl

* Common Issues:
	* Make sure path have changed from "\" to "/"
	* Make sure Proxy setting properly in both of "HTTP Request Defaults" and "phantomJS Driver Config"
		* Proxy: infraproxy.tower.lan : 8080

* Test Result: Copy and Paste LinuxLG-log.jtl and All of csv files in "TestResult" folder from LG to Local, Read them in Jmeter.  

## Logging
### Integration Log - Azure Portal - App Insights

### Function Log - Azure Portal - Functions

### PAS DB - PAS DBA - Ahbishek, Shuja 

## Monitoring
### Integration - App Insights - Daniel

### PEGA - To be confirmed - Praveen / Ashok

### PAS DB - Ahbishek

