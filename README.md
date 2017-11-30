# owf-data-co-municipalities #

This repository contains the [Open Water Foundation (OWF)](http://openwaterfoundation.org) dataset for Colorado municipalities.
This is a foundational dataset that provides unique identifiers and other data for municipalities.
The identifiers can be used to link other datasets, such as water providers that serve municipalities.
OWF has created and is maintaining this dataset to facilitate work on various data analysis and visualization projects in Colorado. 

## Repository Contents ##

The repository contains the following:

```text
analysis/                         		TSTool software command files to process data into useful forms.
  Process-xlsx-to-csv.TSTool			TSTool command file that processes the core dataset from .xlsx to .csv.
  Process-xlsx-to-geojson.TSTool		TSTool command file that processes the core dataset from .xlsx to .geojson.  
data-orig/					Folder containing original data files downloaded from agency websites.
  Colorado-FIPS-Places.csv			The data file containing original data download from the U.S. Census Bureau containing FIPS IDs.
  Colorado-GNIS-Civil.csv			The data file containing original data download from the Geographic Names Information System containing GNIS IDs.
  Colorado-DOLA-LocalGovt-IDs-Municipality.csv		The data file that is a copy of the Department of Local Affairs' Local Government Information System website that contains local government IDs (DOLA_LG_ID).
  Colorado-PWS-IDs.csv				The data file containing original data download from the EPA's Safe Drinking Water Information System containing PWS IDs.
  Colorado-Municipality-PointLocation.csv		Saved attribute table of [Municipal Boundaries in Colorado](https://data.colorado.gov/Municipal/Municipal-Boundaries-in-Colorado/u943-ics6) geojson file that contains coordinates of the centroid of each municipality's boundaries.
data/                           		Folder containing data files.
  Colorado-Municipalities.xlsx     	Simple Excel file containing core data.
  Colorado-Municipalities.csv      	The Excel file contents from the Municipality worksheet converted to a csv file, useful for automated processing.
  Colorado-Municipalities.geojson	The Excel file contents from the Municipality worksheet converted to a geojson file, useful for mapping applications.
  Municipality-County-Relate.csv		The Excel file contents from the Municipality_County_Relate worksheet converted to a csv file, useful for automated processing.
doc/
  ?                             		Additional documentation for the dataset.
.gitattributes                  		Git configuration file indicate repository configuration, in particular handling of line-ending and binary files.
.gitignore                      		Git configuration file to ignore files that should not be committed to the repository.
README.md                     		Explanation of repository contents, data files and sources and TSTool command files used to process the core data into other products.
```

### Colorado-Municipalities.xlsx Contents ###

The core Excel workbook that serves as the master data contains the following data columns within the **Municipality** worksheet.

* **MunicipalityName** -- name of the municipality
* **FIPS_ID** -- 5-digit [Federal Information Processing Standard](https://www.census.gov/geo/reference/codes/place.html) code, to link federal datasets
* **FIPS_ID_Flag** -- data status of FIPS_ID values; see more detail below
* **GNIS_ID** -- [Geographic Names Information System](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) identifier, to link federal datasets
* **GNIS_ID_Flag** -- data status of GNIS_ID values; see more detail below
* **DOLA_LG_ID** -- 5-digit identifier used by Colorado's [Department of Local Affairs (DOLA)](https://dola.colorado.gov/lgis/municipalities.jsf), to link DOLA datasets
* **DOLA_LG_ID_Flag** -- data status of DOLA_LG_ID values; see more detail below
* **BNDSS_ID** -- Basin Needs Decision Support System identifier, also used in [Water Efficiency Data Portal](http://cowaterefficiency.com/unauthenticated_home), to link Colorado Water Conservation Board datasets
* **BNDSS_ID_Flag** --  data status of BNDSS_ID values; see more detail below
* **PWS_ID** -- [Public Water System](https://ofmpub.epa.gov/apex/sfdw/f?p=108:1:::NO:::) identifier, to link Environmental Protection Agency and [Colorado Department of Public Health and Environment](https://www.colorado.gov/pacific/cdphe/data) datasets
* **PWS_ID_Flag** -- data status of PWS_ID values; see more detail below
* **DWR_WaterDistrict_ID -- TO BE ADDED**
* **DWR_WaterDistrict_ID_Flag -- TO BE ADDED**
* **County_CSV** -- county in which the municipality is contained.  Several municipalities are in more than one county.  In these cases, each county is listed in alphabetical order, separated by commas.  Municipalities in multiple counties can also be found in the **Municipality_County_Relate** worksheet.
* **NumCounty** -- number of counties within the municipality's boundaries.  This is a quick way to determine if the municipality is in multiple counties.
* **IBCC_Basin_CSV --  TO BE ADDED**
* **Num_IBCC_Basin --  TO BE ADDED**
* **Latitude** -- latitude of municipality's point location in decimal degrees
* **Longitude** -- longitude of municipality's point location in decimal degrees
* **Lat_Long_Flag** -- indication of how latitude and longitude were determined
* **Comment** -- any other information about the municipality

Each type of identifier also contains a data column of the same name with the word "Flag" added to the column name.  These columns are an indication of data status as it relates to missing data.  The following conventions are used:
* G = ID is a known/good value.  
* g = ID is an estimated (but good) value.  The associated ID cell is also highlighted in yellow.
* N = ID is not applicable for the municipality and a blank cell is expected.
* M = ID is known to be missing in original source and therefore a blank cell indicates that a value cannot be provided.
* m = ID is estimated to be missing.  The associated ID cell is also highlighted in gray.
* z = ID is unable to be confirmed.  A value is possible but cannot be confirmed one way or the other.  The associated ID cell is also highlighted in orange.
* x = OWF has not made an attempt to populate the cell at this time.  The value is missing because OWF has not attempted to find the value.  The associated cell is also highlighted in black.
* C = BNDSS_ID has been newly created based on BNDSS_ID naming conventions (applies to BNDSS IDs only)

Column names are taken from original sources if possible.  For clarity and attribution, agency abbreviations may be added to the original column name.  Column name length is not restricted, therefore, some data representations such as Esri shapefiles may contain truncated column names.  In such cases, alternative formats such as GeoJSON are recommended.

Descriptions of identifiers are also provided in the **Notes** worksheet within the workbook.  This worksheet also details how the original data were downloaded and where to find those files.


Other worksheets within the workbook contain the following:

* **Municipality_County_Relate** worksheet lists the municipalities that are contained in more than one county.  This worksheet is organized so that each county within a municipality is its own record.  Therefore, the same municipality may be listed in more than one row and be associated with a different county.  This will allow for the establishment of one-to-many relationships when linking to and processing other datasets.

* **County** worksheet is simply a list of all of the counties in Colorado.  It is used to fill in county data in other worksheets to ensure data consistency, i.e., no grammatical errors when typing in a county name.

* **Basin** worksheet is simply a list of the Interbasin Compact Committee (IBCC) river basins in Colorado.  It is used to fill in basin data in other worksheets to ensure data consistency, i.e., no grammatical errors when typing in a basin name.

* **ChangeLog** worksheet indicates any changes made to the dataset, the date they occurred and who made the changes.

* **Metadata_Municipality** worksheet serves as the metadata for data columns in the **Municipality** worksheet.


### Colorado-Municipalities.csv Contents ###

This file is the **Municipality** worksheet saved in csv format.  To use this file, **do not** first open in Excel, because IDs that contain leading zeroes will not show those zeroes.  Instead, import the file into a blank Excel file by selecting Data/Get External Data/From Text.


### Municipality_County_Relate.csv Contents ###

This file is the **Municipality_County_Relate** worksheet saved in csv format.  To use this file, **do not** first open in Excel, because IDs that contain leading zeroes will not show those zeroes.  Instead, import the file into a blank Excel file by selecting Data/Get External Data/From Text.


### Colorado-Municipalities.geojson Contents ###

This file is the **Municipality** worksheet saved in GeoJSON format.  This file should be viewable as a map in the GitHub repository.  It can also be used in GIS or mapping applications.

## Attribution ##

The data sources for this dataset are listed below.

* Data available from the [U.S. Census Bureau](https://www.census.gov/geo/reference/codes/place.html) includes municipal Federal Information Processing Standard (FIPS) codes.
* The U.S. Geological Survey (USGS)'s [Geographic Names Information System (GNIS)](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) is the Federal and national standard for geographic nomenclature.  The USGS developed the GNIS in support of the U.S. Board on Geographic Names as the official repository of domestic geographic names data.  OWF manually cross-referenced the Feature Name column to the MunicipalityName.
* The Colorado Department of Local Affairs (DOLA)'s [Local Government Information System](https://dola.colorado.gov/lgis/municipalities.jsf) uses a local government ID (LG ID).  Data were copied directly from the website and pasted into Excel.  OWF manually cross-referenced the LG ID to the MunicipalityName.  OWF is using DOLA_LG_ID instead of LG ID to add more description to the identifier.
* The Environmental Protection Agency (EPA)'s [Safe Drinking Water Information System (SDWIS)](https://ofmpub.epa.gov/apex/sfdw/f?p=108:1:::NO:::) contains information about Public Water System IDs (PWS ID).  PWS IDs are used for water quality reports.  The Colorado Department of Public Health and Environment (CDPHE)'s Water Quality Control Division also uses the PWS ID.  Not all municipalities have a PWS ID.  
In these instances, the municipality's water and sanitation district may have a PWS ID, or the municipality may be served by a water company that has a PWS ID.  OWF manually cross-referenced the PWS Name to the MunicipalityName.
* The BNDSS ID is from the Basin Needs Decision Support System, which was initially developed as a project for the Colorado Water Conservation Board (CWCB) from 2009-2011.  The BNDSS resulted in a prototype gap analysis 
(the difference between water demand and available supply for Colorado) and a prototype database and website to manage water provider and Identified Projects and Processes data.  The BNDSS ID is included in this dataset
so that it can be potentially linked to datasets that result from the Statewide Water Supply Initiative (SWSI) Update.
* Latitude and Longitude coordinates were found by accessing a Colorado Information Marketplace map titled [Municipal Boundaries in Colorado](https://data.colorado.gov/Municipal/Municipal-Boundaries-in-Colorado/u943-ics6).  The map was downloaded as a GeoJSON file and opened in QGIS.  The centroid of each municipality's polygon was calculated and used as the point location for the municipality.

## How to Use the Data ##

The Colorado Municipalities dataset provides a complete statewide list of municipalities assembled from multiple sources.  There are several unique identifiers for each municipality and the dataset allows cross-referencing the identifiers
so that other datasets can be joined.  For example, the [Colorado Water Providers dataset](owf-data-co-municipal-water-providers) uses the municipalities' identifiers and can be used to link additional data.

The Excel or csv files can be used as tabular datasets as is, to create filtered lists or to link to other datasets.  Data-processing software such as TSTool can be used to link this dataset to other datasets.  Datasets can be used within GIS software to create maps.

The format and contents of the dataset will change over time.  It is recommended to save a copy of the dataset.

## License ##

The license is being determined.  All the data are public so there are not really any restrictions on use.

## Contributing ##

The Open Water Foundation is adding value by cross-referencing datasets.
If you use the dataset and have comments, please contact the maintainers and/or use the GitHub issues to provide feedback.

## Maintainers ##

Kristin Swaim (@kswaim, kristin.swaim@openwaterfoundation.org) is the primary maintainer at the Open Water Foundation.

Steve Malers (@smalers, steve.malers@openwaterfoundation.org) is the secondary contact.

## Contributors ##

None yet, other than OWF staff.