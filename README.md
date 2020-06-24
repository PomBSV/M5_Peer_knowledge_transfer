
## Case study 
# Architecture of activities related to financial assessement and projectios of the SB insurance

**Author** : Maya Polanco

**Date**: 29.06.2020 
 
## Objective:
Develop an alternative architecture for the activities relating the financial calculations of the supplementary benefits insurance.
 
## Initial situation

![Image of EL fin-process](images/SB_process.png?raw=true)


-    Budget production : each year new statistics are injected in the model from the year before. The data which is used for assessement or for keeping the data basis are kept separately.
-    Calculations are done in a two steps basis. An R package has been created. This package contains 12 modules which allows us to prepare an excel file with the outputs.
-    The output for the excel sheet where the outputs are pasted is prepared with a format managed by hand.
-    The basis for the projections are the population and disable population scenarios.
-    A mode with statistical data is not yet implemented. However, analysis in a structure different of the this package, are done in an annual basis using package ‘forecast’ in R.
-    In a yearly basis, each second quarter, an analysis using the projections on t and the projections of the year before are done. 
 
### Package massmod_el :
-	12 Module package in R, ccnsisting on 3 modules where the architecture for the projections is managed, and 9 modules which contain functions to execute operations exclusively for this package.
Module input_el : copy from the excel worksheet the inputs for the model
Module comp_el : all the computations are done in this module
Module makeout_el : this module copy all the results in the worksheet.

-	Packages which are used are not supported any more : RDCOMClient.
- Function created to read and write in the package
-	Operational time for 1 execution changes between 4 and 6 minutes per execution.

### FH_EL.xlsx file :
- Output file of the package where projections for the years from actual year until year + 65 are automatically pasted.  , these come from the worksheet output of the projections (package R).
- The objective of this worksheet is to make accessible many inputs which could be used during the year to produce other models.
- One worksheet is produced for each package execution. Format of each sheet in the utput worksheet has to be prepared manually.
- A worksheet is produced 4 times a year or depending on the number of economic scenarios.
- The second quarter analysis between the projections t and t-1 is carried out on a sheet of this file.

### base_el.xlsx file :
- File where projections for the years from actual year until year + 4 are copied by hand , these come from the worksheet output of the projections (package R).
- The objective of this worksheet is to keep a record that is easily accessible. THis worksheet is updated at least four times a year.
- In the second quater, graphics representing the forecasts and the statistics are included and the links have to be updated each year by hand.
- One file is mantained during the years. 

Another structure is used, from where in 2nd. quarter a forecast is handled. This structure has been created separated from the package. Inputs come in part from the base_el.xlsx file and ouputs have no relation with the ones used in the package.


## Initial contributions
- A quick and temporal solution is needed with respect to functions which depends on packages that are not more supported. Some functions from the package as

`openxlsx::writeData` still there is the problem of convertimg the actual ranges in the original function which are described by a letter and a number for example as B12 or C13:D15
```markdown
SpreadsheetWriteW(M, name, RANGE, SHEET)

```
The functions from openxlsx packeage perfomr well and are well supported. An idea would be create a function to convert all these range based format to the one that the writeData funtion from openxlsx package use

```markdown
openxlsx::writeData(wb,ws,data_to_paste, startRow = nb_row, startCol = nb_col)

```
- Modularisation per types of outputs. Original package has just 3 calculation modules, the 9 other modules are functions. The 3 big modules contain code that could be separeted in different modules which could make the program more flexible, when errors appear.
- Modularisation in the same package of activities related to data recording and 
