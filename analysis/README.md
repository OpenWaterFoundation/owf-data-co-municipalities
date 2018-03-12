# analysis #

The `analysis` folder contains TSTool software command files that process data into useful forms.  Each file is described below, with bullets detailing the specific commands used to process data.

## Process-xlsx-to-csv.TSTool ##

This file is a TSTool command file that processes the core dataset (Colorado-Municipalities.xlsx, "Municipality" worksheet) from .xlsx to .csv.
The file contains the following commands.

For the "Municipality" worksheet:
* **ReadTableFromExcel()** - reads the "Municipality" worksheet from Colorado-Municipalities.xlsx as a table into TSTool.  Any blank rows of data are excluded to make sure that the dataset file size is not unnecessarily large.  Data types are specified, such as FIPS_ID being set to "Text" so that leading zeroes are preserved.
* **WriteTableToDelimitedFile()** - saves the "Municipality" worksheet from Colorado-Municipalities.xlsx in CSV format.

For the "Municipality_County_Relate" worksheet:
* **ReadTableFromExcel()** - reads the "Municipality_County_Relate" worksheet from Colorado-Municipalities.xlsx as a table into TSTool.  Any blank rows of data are excluded to make sure that the dataset file size is not unnecessarily large.  Data types are specified, such as DOLA_LG_ID being set to "Text" so that leading zeroes are preserved.
* **WriteTableToDelimitedFile()** - saves the "Municipality_County_Relate" worksheet from Colorado-Municipalities.xlsx in CSV format.

For the "Municipality_Basin_Relate" worksheet:
* **ReadTableFromExcel()** - reads the "Municipality_Basin_Relate" worksheet from Colorado-Municipalities.xlsx as a table into TSTool.  Any blank rows of data are excluded to make sure that the dataset file size is not unnecessarily large.  Data types are specified, such as DOLA_LG_ID being set to "Text" so that leading zeroes are preserved.
* **WriteTableToDelimitedFile()** - saves the "Municipality_Basin_Relate" worksheet from Colorado-Municipalities.xlsx in CSV format.

For the "Municipality_Document_Relate" worksheet:
* **ReadTableFromExcel()** - reads the "Municipality_Document_Relate" worksheet from Colorado-Municipalities.xlsx as a table into TSTool.  Any blank rows of data are excluded to make sure that the dataset file size is not unnecessarily large.  Data types are specified, such as DOLA_LG_ID being set to "Text" so that leading zeroes are preserved.
* **WriteTableToDelimitedFile()** - saves the "Municipality_Document_Relate" worksheet from Colorado-Municipalities.xlsx in CSV format.


## Process-xlsx-to-csv.TSTool ##

This file is a TSTool command file that processes the core dataset (Colorado-Municipalities.xlsx, "Municipality" worksheet) from .xlsx to .geojson.
The file contains the following commands.

* **ReadTableFromExcel()** - reads the "Municipality" worksheet from Colorado-Municipalities.xlsx as a table into TSTool.  Any blank rows of data are excluded to make sure that the dataset file size is not unnecessarily large.  Data types are specified, such as FIPS_ID being set to "Text" so that leading zeroes are preserved.
* **WriteTableToGeoJSON()** - saves the "Municipality" worksheet from Colorado-Municipalities.xlsx in GEOJSON format.  Latitude and longitude data fields are specified.