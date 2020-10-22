# analysis #

The `analysis` folder contains TSTool software command files that process data into useful forms.
ach file is described below, with bullets detailing the specific commands used to process data.

## `process-xlsx-to-csv.tstool` ##

This file is a TSTool command file that processes the core dataset
(Colorado-Municipalities.xlsx, "Municipality" worksheet) from .xlsx to .csv.
The file contains the following commands.

For the `Municipality` worksheet:
* `ReadTableFromExcel` - reads the `Municipality` worksheet from `Colorado-Municipalities.xlsx` as a table into TSTool.
Blank rows of data are excluded.
Data types are specified, such as `FIPS_ID` being set to text so that leading zeroes in identifiers are preserved.
* `WriteTableToDelimitedFile` - saves the `Municipality` worksheet from `Colorado-Municipalities.xlsx` in CSV format.

For the `Municipality_County_Relate` worksheet:
* `ReadTableFromExcel` - reads the `Municipality_County_Relate` worksheet from `Colorado-Municipalities.xlsx` as a table into TSTool.
Blank rows of data are excluded.
Data types are specified, such as `DOLA_LG_ID` being set to text so that leading zeroes in identifiers are preserved.
* `WriteTableToDelimitedFile` - saves the `Municipality_County_Relate` worksheet from
`Colorado-Municipalities.xlsx` in CSV format.

For the `Municipality_Basin_Relate` worksheet:
* `ReadTableFromExcel` - reads the `Municipality_Basin_Relate` worksheet from `Colorado-Municipalities.xlsx` as a table into TSTool.
Blank rows of data are excluded.
Data types are specified, such as `DOLA_LG_ID` being set to text so that leading zeroes in identifiers are preserved.
* `WriteTableToDelimitedFile` - saves the `Municipality_Basin_Relate` worksheet from `Colorado-Municipalities.xlsx` in CSV format.

For the `Municipality_Document_Relate` worksheet:
* `ReadTableFromExcel` - reads the `Municipality_Document_Relate` worksheet from `Colorado-Municipalities.xlsx` as a table into TSTool.
Blank rows of data are excluded.
Data types are specified, such as `DOLA_LG_ID` being set to text so that leading zeroes in identifiers are preserved.
* `WriteTableToDelimitedFile` - saves the `Municipality_Document_Relate` worksheet from `Colorado-Municipalities.xlsx` in CSV format.


## `process-xlsx-to-csv.tstool` ##

This file is a TSTool command file that processes the core dataset (`Colorado-Municipalities.xlsx`,
`Municipality` worksheet) from `.xlsx` to `.geojson`.
The file contains the following commands.

* `ReadTableFromExcel` - reads the `Municipality` worksheet from `Colorado-Municipalities.xlsx` as a table into TSTool.
Blank rows of data are excluded.
Data types are specified, such as `FIPS_ID` being set to text so that leading zeroes in identifiers are preserved.
* `WriteTableToGeoJSON` - saves the `Municipality` worksheet from `Colorado-Municipalities.xlsx` in GEOJSON format.
Latitude and longitude data fields are specified.
