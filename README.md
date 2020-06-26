
## Case study 
# Architecture of activities related to financial assessement and projectios of the SB insurance


**Author** : Maya Polanco

**Date**: 29.06.2020 
 
## Objective:
Develop an alternative architecture for the activities related to the financial calculations of the supplementary benefits insurance.
 
## Initial situation

![Image of EL fin-process](images/SB_process.png?raw=true)


-    Budget production: each year, new statistics are entered in the model from the year before. The data which is used for assessement or for keeping the data basis are kept separately.
-    An R package has been created. This package contains 12 modules which allows us to prepare an output in format .xlsx.
-    Format of the output-worksheet (lines, spaces, etc) is made manually.
-    The basis for the projections are the population and disable population scenarios.
-    A model with statistical data is not yet implemented in this package. However, a forecat-analysis is carried-out in a different structure (R). This forecast-analysis is carried-out in a yearly basis using R package ‘forecast’.
-    Each second quarter, an analysis using the projections on t and the projections of t-1 (year before) are done. This analysis is performed to control changes in the  projections as a consequence of changes in macroeconomic parameters. When a change in projections is observed, a mutation-entry is made in the accounting system (SAP).
-    Another package (delfin) exists to handle projections in the other insurances. Some input data used for different process for the SB insurance come from the same source (FSO) but not from the same general basis existing already for the package delfin. There are different entries of the same data, from the same sources but for different purposes. 
-    Double registration and data entry as : population data, macroeconomic values (wage and price indexes). This data is already existing in a well-managed register of the package delfin. 

### Package massmod_el :
-	12 Module package in R, consisting of 3 modules where the projections calculations are managed, and 9 modules which contain functions to execute operations exclusively for this package.
Module input_el : copy from the excel worksheet the inputs for the model
Module comp_el : all the computations are done in this module
Module makeout_el : this module copy all the results in the worksheet.

-	Packages that are used are no longer supported: RDCOMClient.
- Function created to read and write in the package take too long.
-	Operational time for 1 execution changes between 4 and 6 minutes per execution.

### FH_EL.xlsx file :
- Output file of the package where projections for future years (from actual year until year + 65) are automatically pasted.  
- The objective of this worksheet is to make accessible many inputs which could be used during the year to produce other models.
- One worksheet is produced for each package execution. The format of each sheet in the output worksheet has to be prepared manually.
- A worksheet is produced 4 times a year or depending on the number of economic scenarios.
- The second quarter analysis between the projections t and t-1 is carried out on a sheet of this file.

### base_el.xlsx file :
- File where projections for the years from actual year until year + 4 are copied by hand, these come from the worksheet output of the projections (package R).
- The objective of this worksheet is to keep a record that is easily accessible. This worksheet is updated at least four times a year.
- In the second quater, graphics representing the forecasts and the statistics are included and the links have to be updated each year by hand.
- One file is mantained during the years. 

Another structure is used, from where in 2nd. quarter a forecast is handled. This structure has been created separated from the package. Inputs come in part from the base_el.xlsx file and ouputs have no relation with the ones used in the package.


## Initial contributions
- A quick and temporal solution is needed with respect to functions which depend on packages that are no longer supported. Some functions from the package as

`openxlsx::writeData` still there is the problem of convert the actual ranges in the original function which are described by a letter and a number for example as B12 or C13:D15
```markdown
SpreadsheetWriteW(M, name, RANGE, SHEET)

```
The functions from openxlsx package perform well and are well supported. An idea would be create a function to convert all these range based format to the one that the writeData funtion from openxlsx package use

```markdown
openxlsx::writeData(wb,ws,data_to_paste, startRow = nb_row, startCol = nb_col)

```
- Modularisation per types of outputs. Original package has just 3 calculation modules, the 9 other modules are functions. The 3 big modules contain code that could be separeted in different modules which could make the program more flexible, when errors appear.
- Modularisation in the same package of the data recording.
- Use of input data from package delfin (population).

## Proposed flow

![Image of EL fin-process](images/SB_process_2.png?raw=true)


```diff
# Last updated Jun 26, 2020 
```
