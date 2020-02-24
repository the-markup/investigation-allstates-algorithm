# How We Analyzed Allstate’s Car Insurance Algorithm

This repository contains code to reproduce the findings featured in our story, ["Suckers List: How Allstate’s Secret Auto Insurance Algorithm Squeezes Big Spenders."](https://themarkup.org/allstates-algorithm/2020/02/25/car-insurance-suckers-list)

Our methodology is described in ["How We Analyzed Allstate’s Car Insurance Algorithm."](https://themarkup.org/allstates-algorithm/2020/02/25/show-your-work-car-insurance-suckers-list) 

The data for this analysis can be found in the `data` folder.

The code for all of the analysis is available in `rmd/allstate-tree-analysis.Rmd`. You will likely need to edit the paths for the `.csv` files.

The code to clean and process the Allstate pdf tables is in the Jupyter Notebook `py/table-extractor.ipynb`. The code for this has already been run.

## Installation

### PDF Extractor

We downloaded the tables in pdf form from the [Maryland SERFF Filing Database](https://filingaccess.serff.com/sfa/home/MD) and turned them into csv files using Python 3.7.3 with a Jupyter notebook, `py/table-extractor.ipynb`. 

We included the cleaned csv files in the folder `data/csv`.

Running this code is optional, since the cleaned csv files are provided.

To run, you must download [tika](https://tika.apache.org/1.10/gettingstarted.html), which is used to convert the pdf files to xml. If you use [brew](https://formulae.brew.sh/formula/tika), you can simply run `brew install tika`. This notebook has been tested on OS X, installation may vary depending on your operating system.

You must also install the appropriate packages by running `pip -r requirements.txt`. 

### Analysis

We merged and analyzed the data using R version 3.6.1 (2019-07-05). To run our code, open `rmd/analysis.Rmd`. We recommend using [RStudio](https://rstudio.com/) for viewing.

## Data

### CGR Premiums Table

This table, found in ALSE-129270805, contains individual pricing data. The table, as we recieved it via public records, can be found in `data/pdf/cgr-premiums-table.pdf`. The cleaned csv file is `data/csv/cgr-premiums-table.csv`.

Allstate provided a data dictionary to Maryland regulators, it is available in `reference/cgr-premiums-table-schema.pdf`. 

The column names we use and the titles they are given in the schema are included below:

| Column | Description |
|--------|-------------|
|`territory`| (1a) Rating Territory|
|`gender`| (1b) Gender of Oldest Operator|
|`birthdate`| (1c) Birthdate of Oldest Operator|
|`ypc`| (1d) Years with Prior Carrier|
|`current_premium`| (2) Current Premium|
|`indicated_premium`| (3) Indicated Premium|
|`selected_premium`| (4) Selected Premium|
|`underlying_premium`| (5a) Underlying Rating Plan Proposed CGR Applicable Coverage Premium|
|`fixed_expenses`| (5b) Proposed Fixed Expense and Other Premium |
|`underlying_total_premium`|(5c) Underlying Rating Plan Proposed Total Premium|
|`cgr_factor`| (6) Selected Group Factor|
|`cgr`| (7) Complementary Group|

### Territory Definitions Table

This table, found in ALSE-129270805, defines the "territories", which are referred to in the CGR Premiums Table. The table, as we recieved it via public records, can be found in `data/pdf/territory-definitions-table.pdf`. The cleaned csv file is `data/csv/territory-definitions-table.csv`.

The column names we use and the column names in the filing documentation are included below:

| Column | Description |
|--------|-------------|
| `county`| County
|`county_code`| County Code
|`territory`| Territory
|`zipcode`| Zip Code
|`town`| Town
|`area`| Area


### CGR Definition Table

This table, found in ALSE-129270805, defines the "Complementary Groups". The table, as we recieved it via public records, can be found in `data/pdf/cgr-definitions-table.pdf`. The cleaned csv file is `data/csv/cgr-definitions-table.csv`.

The column names we use and the column names in the filing documentation are included below:

| Column | Description |
|--------|-------------|
| `cgr`       | Complementary Group|
| `aa`       | AA |
| `bb`       | BB |
| `cc`       | CC |
| `va`       | VA |
| `dd`       | DD |
| `hh`       | HH |
| `ss`       | SS |

The column names correspond to those found in the worksheet used to calculate a policyholder's premium, see `reference/premium-calcluation-sheet.pdf` for one included in ALSE-129270805. 

### US Census 2011-2015 American Community Survey 5-Year Estimates Data

We used ZCTA-level data from US Census 2011-2015 American Community Survey 5-Year Estimates to do race and income analyses. We include a copy of "DP03 - Selected Economic Characteristics" (`data/csv/ACS_MD_15_5YR_DP03.csv`) and "DP05 - ACS Demographic and Housing Estimates" (`data/csv/ACS_MD_15_5YR_DP05.csv`) for ZCTA codes fully or partially in Maryland.

## Licensing

Copyright 2020, The Markup News Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.