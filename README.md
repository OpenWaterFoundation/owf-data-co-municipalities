# owf-data-co-municipalities #

This repository contains the [Open Water Foundation (OWF)](http://openwaterfoundation.org) dataset for Colorado municipalities.
This is a foundational dataset that provides unique identifiers and other data for municipalities.
The identifiers can be used to link other datasets, such as water providers.
OWF has created and is maintaining this dataset to facilitate work on various data analysis and visualization projects in Colorado.

## Repository Contents ##

The repository contains the following:

```text
.gitignore                      Git configuration file to ignore files that should not be committed to the repository.
.gitattributes                  Git configuration file indicate repository configuration, in particular handling
                                of line-ending and binary files.
build/
                                Folder used by TSTool to create products for publication.
data/                           Folder containing data files.
  Colorado_Municipalities.xlsx  Simple Excel file containing core data.
  Colorado_Municipalities.csv   The Excel file contents converted to a csv file, useful for automated processing.
doc/
  ?                             Additional documentation for the dataset.
TSTool/                         TSTool software command files to process data into useful forms.
  README.md                     Explanation of TSTool command files used to process the core data into other products.
```

### Colorado_Municipalities.xlsx Contents ###

The core Excel workbook that serves as the master data contains the following data columns.  Descriptions of identifiers are provided in the Attribution section and also in the Notes worksheet within the workbook.

* Municipality_Name -- name of the municipality
* FIPS_ID -- Federal Information Processing Standard code
* LocalGovt_ID -- identifier used by Colorado's Department of Local Affairs (DOLA)
* BNDSS_ID -- Basin Needs Decision Support System identifier
* PWS_ID -- Public Water System identifier
* County -- county(s) in which the municipality is contained
* Basin -- IBCC basin(s) in which the municipality is contained
* Comment -- OWF comments, particularly regarding the creation of BNDSS IDs for municipalities that previously did not have a BNDSS ID. 

## Attribution ##

The data sources for this dataset are listed below.

* The list of Colorado municipalities was downloaded from the [U.S. Census Bureau](https://www.census.gov/geo/reference/codes/place.html) in February 2017.  The data available from the Census Bureau
includes municipal Federal Information Processing Standard (FIPS) codes as well as the county(s) in which the municipality is contained.
* The list of municipalities was then cross-checked with the Colorado Department of Local Affairs (DOLA)'s [Local Government Information System](https://dola.colorado.gov/lgis/municipalities.jsf).
DOLA uses a local government ID (LG ID).  OWF is using LocalGovt_ID instead of LG ID to add more description to the identifier.
* The Environmental Protection Agency (EPA)'s [Safe Drinking Water Information System (SDWIS)](https://ofmpub.epa.gov/apex/sfdw/f?p=108:1:::NO:::) contains information about Public Water System IDs (PWS ID).
PWS IDs are used for water quality reports.  The Colorado Department of Public Health and Environment (CDPHE)'s Water Quality Control Division also uses the PWS ID.  Not all municipalities have a PWS ID.  In these instances, the municipality's water and sanitation district may have a PWS ID, or the municipality may be served by a water company that has a PWS ID.
* The BNDSS ID is from the Basin Needs Decision Support System, which was initially developed as a project for the Colorado Water Conservation Board (CWCB) from 2009-2011.  The BNDSS resulted in a prototype gap analysis 
(the difference between water demand and available supply for Colorado) and a prototype database and website to manage water provider and Identified Projects and Processes data.  The BNDSS ID is included in this dataset
so that it can be potentially linked to datasets that result from the Statewide Water Supply Initiative (SWSI) Update.

## How to Use the Data ##

The Colorado municipalities dataset provides a complete statewide list of municipalities assembled from multiple sources.
There are several unique identifiers for each municipality and the dataset allows cross-referencing the identifiers
so that other datasets can be joined.
For example, the [Colorado water providers dataset](owf-data-co-municipal-water-providers) dataset uses the municipalities'
identifiers to indicate which municipalities a water provider serves.

The Excel or csv forms can be used as tabular datasets as is, or to link to other datasets.

## License ##

The license is being determined.
All the data are public so there are not really any restrictions on use.

## Contributing ##

The Open Water Foundation is currently working on an initial release of the dataset to support a
data visualization project in the South Platte Basin of Colorado.
If you use the dataset and have comments, please contact the maintainers and/or use the GitHub issues to provide feedback.

## Maintainers ##

Kristin Swaim (@kswaim, kristin.swaim@openwaterfoundation.org) is the primary maintainer at the Open Water Foundation.

Steve Malers (@smalers, steve.malers@openwaterfoundation.org) is the secondary contact.

## Contributors ##

None yet, other than OWF staff.
