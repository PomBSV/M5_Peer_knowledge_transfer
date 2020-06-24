
## Case study 
# Architecture of the activities related to financial assessement and projectios of the SB insurance

**Author** : Maya Polanco

**Date**: 29.06.2020 
 
## Objective:
Develope an alternative architecture for the activities relating the financial calculations of the supplementary benefits insurance.
 
## Initial situation

![Image of EL fin-process](images/SB_process.png?raw=true)


-    Budget production : each year new statistics are injected in the model from the year before. The data which is used for assessement or for keeping the data basis are kept separately.
-    Calculations are done in a two steps basis. An R package has been created. This package contains 12 modules which allows us to prepare an excel file with the outputs.
-    The output for the excel sheet where the outputs are pasted is prepared with a format managed by hand.
-    The basis for the projections are the population and disable population scenarios.
-    A mode with statistical data is not yet implemented. However, analysis in a structure different of the this package, are done in an annual basis using package ‘forecast’ in R.
-         
 
### Package massmod_el :
-	12 Module package in R, ccnsisting on 3 modules where the architecture for the projections is managed, and 9 modules which contain functions to execute operations exclusively for this package.
Module input_el : copy from the excel worksheet the inputs for the model
Module comp_el : all the computations are done in this module
Module makeout_el : this module copy all the results in the worksheet.

-	Packages which are used are not supported any more : RDCOMClient, …
-	Operational time for 1 execution changes between 4 and 6 minutes per execution.

### base_el file :
- File where projections for the years from actual year until year + 4 are copied by hand , these come from the worksheet output of the projections (package R)

## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/PomBSV/exam/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.



```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/PomBSV/exam/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
