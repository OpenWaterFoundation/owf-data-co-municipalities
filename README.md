# owf-data-co-municipalities #

This repository contains the [Open Water Foundation (OWF)](https://openwaterfoundation.org) dataset for Colorado municipalities.
This is a foundational dataset that provides unique identifiers and other data for municipalities.
The identifiers can be used to link other datasets,
including population datasets and water providers that serve municipalities.
OWF has created and is maintaining this dataset to facilitate work on various data analysis and visualization projects in Colorado. 

The following sections provide a summary of the project repository:

* [Repository Contents](#repository-contents)
* [`Colorado-Municipalities.xlsx` Contents](#colorado-municipalitiesxlsx-contents)
    + [Worksheet Columns](#worksheet-columns)
    + [Identifier Conventions for OWF_ID](#identifier-conventions-for-owf_id)
    + [Data Flags](#data-flags)
    + [Worksheet Conventions](#worksheet-conventions)
    + [Worksheets in Workbook](#worksheets-in-workbook)
* [Data Files](#data-files)
* [How to Use the Data](#how-to-use-the-data)
* [Attribution](#attribution)
* [Dataset Workflow](#dataset-workflow)
* [Disclaimer](#disclaimer)
* [License](#license)
* [Maintainers and Contributing](#maintainers-and-contributing)

-------------------------

## Repository Contents ##

The repository contains the following:

```text
.gitattributes                                  Git configuration file indicate repository configuration,
                                                in particular handling of line-ending and binary files.
.gitignore                                      Git configuration file to ignore files that should not be committed to the repository.
README.md                                       Explanation of repository contents, data files and sources and
                                                TSTool command files used to process the core data into other products.
data/                                           Folder containing data files.
  co-municipalities.xlsx                        Simple Excel file containing core data.
  co-municipalities.csv                         The Excel file contents from the Municipality worksheet
                                                converted to a csv file, useful for automated processing.
  co-municipalities.geojson                     The Excel file contents from the Municipality worksheet
                                                converted to a geojson file, useful for mapping applications.
  co-municipalities-basin-relate.csv            The Excel file contents from the Municipality_Basin_Relate worksheet
                                                converted to a csv file, useful for automated processing.
  co-municipalities-county-relate.csv           The Excel file contents from the Municipality_County_Relate worksheet
                                                converted to a csv file, useful for automated processing.
  co-municipalities-document-relate.csv         The Excel file contents from the Municipality_Document_Relate worksheet
                                                converted to a csv file, useful for automated processing.
data-orig/                                      Folder containing original data files downloaded from agency websites.
  Colorado-DOLA-LocalGovernment-Municipalities.tsv
                                                Copy and pasted from:  https://dola.colorado.gov/lgis/municipalities.jsf
                                                This is a newer download than the originally downloaded file:
                                                Colorado-DOLA-LocalGovt-IDs-Municipality.csv
  Colorado-DOLA-LocalGovernment-Municipalities.csv
                                                The above file saved as csv.
  Colorado-DOLA-LocalGovt-IDs-Municipality.csv  The data file that is a copy of the Department of Local Affairs' (DOLA)
                                                Local Government Information System website that contains local government IDs
                                                (DOLA_LG_ID).  See DOLA attribution below.
                                                THIS FILE MAY BE REMOVED IN THE FUTURE AS THE ABOVE VERSION IS PHASED IN.
  Colorado-FIPS-Places.csv                      The data file containing original data download from the
                                                U.S. Census Bureau containing FIPS IDs.
  Colorado-GNIS-Civil.csv                       The data file containing original data download from the
                                                Geographic Names Information System containing GNIS IDs.
  Colorado-Municipality-PointLocation.csv       Saved attribute table of Municipal Boundaries in Colorado geojson file
                                                downloaded from the Colorado Information Marketplace that contains
                                                coordinates of the centroid of each municipality's boundaries.
  Colorado-PWS-IDs.csv                          The data file containing original data download from the EPA's
                                                Safe Drinking Water Information System containing PWS IDs.
  README.md                                     Explanation of folder contents, description of data files,
                                                and the methodology used to obtain the data and mapping to the joined dataset
data-orig-workflow/                             Folder containing files, such as TSTool command files,
                                                for processing original data into usable formats.
  downloads/                                    Dynamically-created folder for downloads, ignored from Git repository.
  process-original-data-to-csv.tstool           TSTool command file that processes files that are automatically downloaded
                                                from websites and data files manually downloaded, which are incorporated
                                                into the main dataset.
doc/                                            Additional documentation for the dataset.
workflow/                                       TSTool software command files to process data into useful forms.
  01-convert-formats.tstool                     TSTool command file to convert the dataset from .xlsx to .csv and .geojson.
x-visualizations/                               Files created for specific visualizations, being evaluated.
                                                NO LONGER USED.
                                                These files may be moved to other repositories that contain visualizations.
z-local-notes/                                  Used for local notes, files are not committed to the repository.
```

## `Colorado-Municipalities.xlsx` Contents ##

### Worksheet Columns ###

The core Excel workbook that serves as the master data contains the following data columns
within the ***Municipality*** worksheet.
Cross-referencing identifiers were added when creating of the workbook. 

| **Column** | **Description** |
| -- | -- |
| **MunicipalityName** | Name of the municipality. |
| **FIPS_ID** | 5-digit [Federal Information Processing Standard](https://www.census.gov/geo/reference/codes/place.html) code, to link federal datasets. |
| **FIPS_ID_Flag** | Data status of FIPS_ID values; see more detail below. |
| **GNIS_ID** | [Geographic Names Information System](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) identifier, to link federal datasets. |
| **GNIS_ID_Flag** | Data status of GNIS_ID values; see more detail below. |
| **DOLA_LG_ID** | 5-digit identifier used by Colorado's [Department of Local Affairs (DOLA)](https://dola.colorado.gov/lgis/municipalities.jsf), to link DOLA datasets. |
| **DOLA_LG_ID_Flag** | Data status of DOLA_LG_ID values; see more detail below. |
| **OWF_ID** | Unique text identifier created by OWF to ensure that every municipality has a unique identifier.  The `OWF_ID` is a concatenation of muninicpality words, using abbreviations. |
| **OWF_ID_Full** | Unique text identifier created by OWF to ensure that every municipality has a unique identifier.  The `OWF_ID` is a concatenation of muninicpality words, using full words. |
| **OWF_ID_Flag** | Data status of OWF_ID values; see more detail below. |
| **PWS_ID** | [Public Water System](https://ofmpub.epa.gov/apex/sfdw/f?p=108:1:::NO:::) identifier, to link Environmental Protection Agency and [Colorado Department of Public Health and Environment](https://www.colorado.gov/pacific/cdphe/data) datasets. |
| **PWS_ID_Flag** | Data status of PWS_ID values; see more detail below. |
| **DWR_WaterDistrict_ID** | **TO BE ADDED** |
| **DWR_WaterDistrict_ID_Flag** | **TO BE ADDED** |
| **County_CSV** | County in which the municipality is contained. For municipalities that are in more than one county consistent with DOLA population data, counties are listed in alphabetical order, separated by commas. Municipalities in multiple counties can also be found in the ***Municipality_County_Relate*** worksheet. |
| **NumCounty** | Number of counties within the municipality's boundaries. | This is a quick way to determine if the municipality is in multiple counties. |
| **IBCC_Basin_CSV** | Interbasin Compact Committee (IBCC) basin in which the municipality is contained. Some municipalities are in more than one basin. In these cases, each basin is listed in alphabetical order, separated by commas.  Municipalities in multiple basins can also be found in the ***Municipality_Basin_Relate*** worksheet. |
| **Num_IBCC_Basin** | Number of IBCC basins within the municipality's boundaries. This is a quick way to determine if the municipality is in multiple basins. |
| **Latitude** | Latitude of municipality's point location in decimal degrees. |
| **Longitude** | Longitude of municipality's point location in decimal degrees. |
| **Lat_Long_Flag** | Indication of how latitude and longitude were determined. |
| **Website** | Website URL of the municipality.  If a website was not found, the corresponding Wikipedia page was used. |
| **Website_Flag** | Data status of Website values; see more detail below. |
| **Comment** | Any other information about the municipality. |

### Identifier Conventions for OWF_ID ###

The following conventions are used to create `OWF_ID` values from longer names.
See the `OWF_ID_Full` identifier for identifier that uses full words rather than abbreviations.

| **Abbreviation** | **Long Version** |
| ---------------- | ---------------- |
| `Crk`            | `Creek`          |
| `Ft`             | `Fort`           |
| `Hls`            | `Hills`          |
| `Hts`            | `Heights`        |
| `Mt`             | `Mount`          |
| `Mtn`            | `Mountain`       |
| `Spgs`           | `Springs`        |
| `Vlg`            | `Village`        |
| `Vly`            | `Valley`         |

### Data Flags ###

Many data columns have an accompanying second column with the same name and
the `_Flag` appended to the original column name.
These columns are an indication of data status as it relates to missing or estimated data values.
The following conventions are used:

| **Flag Value** | **Description** |
| --- | -- |
| `G` | Value is a known/good value. |
| `g` | Value is an estimated (but good) value.  The associated cell is also highlighted in yellow. |
| `N` | Value is not applicable for the municipality and a blank cell is expected. |
| `M` | Value is known to be missing in original source and therefore a blank cell indicates that a value cannot be provided. |
| `m` | Value is estimated to be missing.  The associated cell is also highlighted in gray. |
| `z` | Value is unable to be confirmed.  A value is possible but cannot be confirmed one way or the other.  The associated cell is also highlighted in orange. |
| `x` | OWF has not made an attempt to populate the cell at this time.  The value is missing because OWF has not attempted to find the value.  The associated cell is also highlighted in black. |

### Worksheet Conventions ###

Colors are only visible in `xlsx` files and not `csv` files.

Column names are taken from original sources if possible.
For clarity and attribution, agency abbreviations may be added to the original column name.
Column name length is not restricted, therefore,
some data representations such as Esri shapefiles may contain truncated column names.
In such cases, alternative formats such as GeoJSON are recommended.

Descriptions of identifiers are also provided in the ***Notes*** worksheet within the workbook.
This worksheet also details how the original data were downloaded and where to find those files.

### Worksheets in Workbook ###

Worksheets within the workbook are as follows:

| **Worksheet** | **Description** |
| -- | -- |
| ***Municipality*** | Main datase.  Municipalities in Colorado, described above. |
| ***Municipality_County_Relate*** | Municipality/county relationships for municipalities that are contained in more than one county. |
| ***Municipality_Basin_Relate*** | Municipality/basin relationships for municipalities that are contained in more than one IBCC basin. |
| ***Municipality_Document_Relate*** | Documents such as water efficiency plans, source water assessment plans, etc. that are associated with a particular municipality.  A URL is provided for each document.  The documents were found by manually searching for documents using the terms "water conservation efficiency plans" and the municipality's name.  This worksheet is organized so that each document is its own record.  A municipality may be listed in more than one row if a municipality is associated with multiple documents.  This worksheet is incomplete but highlights the potential for providing links to any documents associated with a municipality. |
| ***County*** | Counties in Colorado, used to fill in county data in other worksheets to ensure data consistency, i.e., no grammatical errors when typing in a county name. |
| ***IBCC_Basin*** | Interbasin Compact Committee (IBCC) river basins in Colorado, used to fill in basin data in other worksheets to ensure data consistency, i.e., no grammatical errors when typing in a basin name. |
| ***ChangeLog*** | Indicates changes to the dataset, the date they occurred and who made the changes. |
| ***Metadata_Municipality*** | Metadata for data columns in the ***Municipality*** worksheet. |

## Data Files ##

Files in the `data/` folder are created by exporting data from the `Colorado-Municipalities.xlsx` workbook as `csv` and `geojson` files.
These files can be used directly without having to process the Excel file.

### `co-municipalities.csv` Contents ###

This file is the ***Municipality*** worksheet saved in csv format.
Warning:  if this file is opened directly in Excel, IDs that contain leading zeroes will not show those zeroes.
Instead, import the file into a blank Excel file by selecting Data/Get External Data/From Text.

### `co-municipalities.geojson Contents ###

This file is the ***Municipality*** worksheet saved in GeoJSON format.
This file is viewable as a map in the GitHub repository.
It can also be used in GIS and mapping applications.

### `co-municipalities-basin-relate.csv` Contents ###

This file is the ***Municipality_Basin_Relate*** worksheet saved in csv format.
Warning:  if this file is opened directly in Excel,
IDs that contain leading zeroes will not show those zeroes.
Instead, import the file into a blank Excel file by selecting Data/Get External Data/From Text.

### `co-municipalities-county-relate.csv` Contents ###

This file is the ***Municipality_County_Relate*** worksheet saved in csv format.
Warning:  if this file is opened directly in Excel,
IDs that contain leading zeroes will not show those zeroes.
Instead, import the file into a blank Excel file by selecting Data/Get External Data/From Text.

### `co-municipalities-document-relate.csv` Contents ###

This file is the ***Municipality_Document_Relate*** worksheet saved in csv format.
Warning:  if this file is opened directly in Excel,
IDs that contain leading zeroes will not show those zeroes.
Instead, import the file into a blank Excel file by selecting Data/Get External Data/From Text.

## How to Use the Data ##

The Colorado Municipalities dataset provides a complete statewide list of municipalities assembled from multiple sources.
There are several unique identifiers for each municipality and the
dataset allows cross-referencing the identifiers so that other datasets can be joined.
For example, the
[Colorado Water Providers dataset](https://data.openwaterfoundation.org/state/co/co-municipal-water-providers) dataset
uses the municipalities' identifiers and can be used to link additional data.
In addition, organizations like the [Colorado Municipal League](https://www.cml.org/) may find the dataset
useful and connections could be made to their data if any of these identifiers are used with their data.

The Excel and csv files can be used as tabular datasets as is, to create filtered lists or to link to other datasets.
Data-processing software such as TSTool can be used to link this dataset to other datasets.
Datasets can be used within GIS software to create maps.

The format and contents of the dataset may change over time.
It is recommended to save a copy of the dataset.

## Attribution ##

The data sources for this dataset are listed below.

| **Data Source** | **Description** |
| -- | -- |
| [U.S. Census Bureau](https://www.census.gov/geo/reference/codes/place.html) | Includes municipal Federal Information Processing Standard (FIPS) codes. |
| U.S. Geological Survey (USGS)'s [Geographic Names Information System (GNIS)](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) | GNIS is the Federal and national standard for geographic nomenclature.  The USGS developed the GNIS in support of the U.S. Board on Geographic Names as the official repository of domestic geographic names data.  OWF manually cross-referenced the Feature Name column to the MunicipalityName. |
| The Colorado Department of Local Affairs (DOLA)'s [Local Government Information System](https://dola.colorado.gov/lgis/municipalities.jsf) local government ID (LG ID) | Data were copied directly from the website and pasted into Excel.  To copy the data highlight the table on the DOLA website and save OWF manually cross-referenced the LG ID to the MunicipalityName.  OWF is using DOLA_LG_ID instead of LG ID to add more description to the identifier. |
| Environmental Protection Agency (EPA)'s [Safe Drinking Water Information System (SDWIS)](https://ofmpub.epa.gov/apex/sfdw/f?p=108:1:::NO:::) Public Water System IDs (PWS ID) | PWS IDs are used for water quality reports.  The Colorado Department of Public Health and Environment (CDPHE)'s Water Quality Control Division also uses the PWS ID.  Not all municipalities have a PWS ID. In these instances, the municipality's water and sanitation district may have a PWS ID, or the municipality may be served by a water company that has a PWS ID.  OWF manually cross-referenced the PWS Name to the MunicipalityName. |
| Open Water Foundation OWF_ID | OWF_ID was created for each municipality by the Open Water Foundation in order to ensure that at least one type of identifier contains values for every municipality.  For example, almost every municipality has a DOLA LG ID, with the exception of Carbonate. However, if Carbonate needed to be linked to other datasets via the DOLA_LG_ID, this would not be possible.  Therefore, the OWF_ID is needed to potentially link every municipality to other datasets.  OWF_ID is used in the "Relate" worksheets and csv files as the identifier for this reason. |
| Latitude and Longitude coordinates from Colorado Information Marketplace. | The map titled [Municipal Boundaries in Colorado](https://data.colorado.gov/Municipal/Municipal-Boundaries-in-Colorado/u943-ics6).  The map was downloaded as a GeoJSON file and opened in QGIS.  The centroid of each municipality's polygon was calculated and used as the point location for the municipality. |
| Municipality Website URLs | URLs were found by manually searching for municipality websites.  Documents such as water efficiency plans were also manually searched. |

## Dataset Workflow ##

The following is a summary of the workflow to create the dataset.
Details for each file are described in the [data-orig/README.md](data-orig/README.md) file.
Steps can be followed if recreating or updating the dataset.
The process can be further automated to streamline the overall workflow;
however, some steps were initially performned manually.

1. Manually create the `Colorado-Municipalities.xlsx` Excel workbook:
    1. Manually populate the empty worksheets (some were added later as data were evaluated).
2. Manually download `data-orig` files:
    1. `Colorado-DOLA-LocalGovernment-Municipalities.tsv` is copy and pasted from
       [https://dola.colorado.gov/lgis/municipalities.jsf](https://dola.colorado.gov/lgis/municipalities.jsf)
       to create a tab-delimited file.  The column headings were manually added.
       The older `Colorado-DOLA-LocalGovt-IDs-Municipality.csv` was created similarly but is being phased out.
       See the automated step below to create the corresponding `csv` file.
    2. `Colorado-GNIS-Civil.psv` was creating by manually downloading from
       [https://geonames.usgs.gov/apex/f?p=138:1::::::](https://geonames.usgs.gov/apex/f?p=138:1::::::)
       using `State=Colorado` and `Feature Class:Civil` (all other fields have default values).
       After querying, save to `Colorado-GNIS-Civil.psv` (pipe-separated-value).
       This file contains municipalities, counties, and other local government entities.
       See the automated step below to create the corresponding `csv` file.
    3. `Colorado-PWS-IDs.csv` was created by manually downloading from
       [https://ofmpub.epa.gov/apex/sfdw/f?p=108:1:::NO:::](https://ofmpub.epa.gov/apex/sfdw/f?p=108:1:::NO:::)
       using `Select a Report=Water System Summary` and `Primacy Agency=Colorado` (all other fields have default values).
       The file was saved as `Colorado-PWS-IDs.csv`.
3. Automate download and process `data-orig` files.
   Run `data-orig-process/process-original-data-to-csv.tstool`, which creates:
    * `data-orig/Colorado-DOLA-LocalGovernment-Municipalities.csv` - DOLA municipalities
    * `data-orig/Colorado-FIPS-Places.csv` - FIPS places including municipalities
    * `data-orig/Colorado-GNIS-Civil.csv` - GNIS civil places including municipalities and counties

## Disclaimer ##

OWF has attempted to create a complete statewide dataset of municipalities.
OWF will attempt to fill data gaps as the dataset is used for analysis and funding allows for more data review.
OWF provides no guarantee as to the accuracy of the data.
**Use this dataset at your own risk.**
OWF welcomes feedback to improve the dataset.

## License ##

This dataset is distributed using the
[Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0) License](https://creativecommons.org/licenses/by-sa/4.0/).
Please provide attribution.

## Maintainers and Contributing ##

This dataset is maintained by the Open Water Foundation.
The Open Water Foundation is adding value by cross-referencing datasets.
If you use the dataset and have comments,
please contact the maintainers and/or use the GitHub issues to provide feedback.
