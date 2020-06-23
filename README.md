
# **Case study** 
Architecture of a new financial perspectives model

Author : Maya Polanco

Date: 29.06.2020 
 
## Objective:
Create a new architecture for the activities relating the financial calculations of the supplementary benefits insurance.
 
## Initial situation

[Image of EL fin-process](https://github.com/PomBSV/exam/images/SB_process.png)

-    Calculations are done in a two steps basis. An R package has been created. This package contains 12 modules which allows us to prepare an excel file with the outputs.
-    9 out of 12 modules contain functions, which has been created exclusively for this package. Packages as: XLConnect, RDCOMClient, are used to 
-    The output for the excel sheet where the outputs are pasted is prepared with a format managed by hand.
-    The basis for the projections are the population and disable population scenarios.
-    A mode with statistical data is not yet implemented. Even though, analysis out of the package, are done in an annual basis using package ‘forecast’ in R.
-         
 
### Some facts :
-	12 Module package in R. 3 modules 
Module input_el : copy from the excel worksheet the inputs for the model
Module comp_el : all the computations are done in this module
Module makeout_el : this module copy all the results in the worksheet.

9 modules contain functions to execute operations.
-	Packages which are used are not supported any more : RDCOMClient, …
-	Operational time of 1 execution changes between 4 and 6 minutes per exécution.
o	Budget production : each year new statistics are injected in the model from the year before. The data which is used for control or for keeping the data basis are kept separately.

bas.xlsx


o	Control of budget in a quarterly basis. Nowadays, a parallele structure has been created to control the Budget. This structure is feeded with data at the end of mars of each year

Solutions
-

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
