# data-orig #

The `data-orig` folder contains original data files downloaded from various websites.
The contents of each file are described below,
as well as the methodology used to obtain the data and mapping to the joined dataset.

## Colorado-DOLA-LocalGovernment-Municipalities.csv ##

This file is a copy of the Department of Local Affairs (DOLA)'s
[Local Government Information System](https://dola.colorado.gov/lgis/municipalities.jsf)
web page that contains local government IDs (DOLA_LG_ID).
Local government IDs are useful for linking DOLA and perhaps other State datasets.
These data are not available in a machine-readable, downloadable format via a direct URL.
Therefore, the data were copied directly from the website data table and
saved to the `Colorado-DOLA-LocalGovernment-Municipalities.tsv` file using a text editor.
It is necessary to treat the identifiers as text to preserve leading zeroes.
The file was [processed using TSTool](https://github.com/OpenWaterFoundation/owf-data-co-municipalities/blob/master/data-orig-process/process-original-data-to-csv.tstool)
command file to translate the `tsv` file into `csv`.

The file contains the following data columns.

| **Column** | **Description** |
| -- | -- |
| **City/Town Name:** | Name of the municipality; text format; manually cross-referenced to the **MunicipalityName** column in the main dataset. |
| **Type:** | Type of municipality; text format; not used in main dataset. |
| **LG ID:** | 5-digit identifier used by DOLA; converted to text format to preserve leading zeroes; is the **DOLA_LG_ID** column in the main dataset. |
| **FIPS:** | 5-digit [Federal Information Processing Standard](https://www.census.gov/geo/reference/codes/place.html) code; converted to text format to preserve leading zeroes; is the **FIPS_ID** column in the main dataset. |
| **Census MRF:** | Census master reference file; integer format; not used in main dataset. |
| **Counties:** | County(s) in which the municipality is contained; text format; already provided in the main dataset. |

Once the "City/Town Name:" column was cross-referenced to the
**MunicipalityName** column in the main dataset,
then the "LG ID:" column was pasted into the main dataset and the column renamed to **DOLA_LG_ID**.

## Colorado-FIPS-Places.csv ##

This file contains original data downloaded from the
[U.S.Census Bureau](https://www.census.gov/geo/reference/codes/place.html)
containing Federal Information Processing Standard (FIPS) IDs for "Places".
FIPS IDs are useful for linking federal datasets.
"Colorado" was selected under the "Select a File" option and the data are available as a
[pipe-delimited file](https://www2.census.gov/geo/docs/reference/codes/files/st08_co_places.txt).
The pipe-delimited file was opened directly in TSTool using the WebGet() command.
The data were [processed using TSTool](https://github.com/OpenWaterFoundation/owf-data-co-municipalities/blob/master/data-orig-process/process-original-data-to-csv.tstool)
to create column headings for the data, remove redundant carriage return characters,
and saved in CSV format as `data-orig/Colorado-FIPS-Places.csv`.

The file contains the following data columns.

| **Column** | **Description** |
| -- | -- |
| **State** | 2-letter state postal code, "CO" for Colorado; not used in main dataset. |
| **StateFP** | 2-digit state FIPS code, "08" for Colorado; not used in main dataset. |
| **PlaceFP** | Place or county subdivision 5-digit FIPS code; converted to text format to preserve leading zeroes; is the **FIPS_ID** column in the main dataset. |
| **PlaceName** | Place or county subdivision name and legal/statistical area description; text format; is the **MunicipalityName** column in the main dataset with "town" or "city" removed from the name. |
| **Type** | Type of place or county subdivision; text format; not used in main dataset. |
| **FuncStat** | Functional status; see website; text format; not used in main dataset. |
| **County** | County(s) in which the place or county subdivision is located; text format; is the **County_CSV** column in the main dataset. |

## Colorado-GNIS-Civil.csv ##

This file contains original data downloaded from the
[Geographic Names Information System (GNIS)](https://geonames.usgs.gov/apex/f?p=138:1:0::NO:::) containing GNIS IDs.
GNIS IDs are useful for linking federal datasets.
"Colorado" was selected for the State and "Civil" for the Feature Class.
The GNIS data were saved as pipe-delimited file `data-orig/Colorado-GNIS-Civil.psv`.
The data were [processed using TSTool](https://github.com/OpenWaterFoundation/owf-data-co-municipalities/blob/master/data-orig-process/process-original-data-to-csv.tstool)
to convert to CSV format as `data-orig/Colorado-GNIS-Civil.csv`.

The file contains the following data columns.

| **Column** | **Description** |
| -- | -- |
| **Feature Name** | Name of either the municipality, county or division, with the words "County", "Division", "Town of" or "City of" contained in the name; text format; manually cross-referenced to the **MunicipalityName** column in the main dataset. |
| **ID** | GNIS ID; converted to text format to preserve leading zeroes; is the **GNIS_ID** column in the main dataset. |
| **Class** | Class of the feature; note that all are "Civil"; not used in main dataset. |
| **County** | County(s) in which the municipality is contained; text format; already provided in the main dataset. |
| **State** | State the feature is located in, "CO" for Colorado; not used in main dataset. |
| **Latitude** | Latitude in degrees-minutes-seconds; integer plus text format; not used in main dataset because of format. |
| **Longitude** | Longitude in degrees-minutes-seconds; integer plus text format; not used in main dataset because of format. |
| **Ele(ft)** | Elevation of the feature, in feet; integer format; not used in main dataset. |
| **Map** | USGS topographic map name; text format; not used in main dataset. |
| **BGN Date** | Board of Geographic Names date; date format; not used in main dataset. |
| **Entry Date** | Date entered into the system; date format; not used in main dataset. |

Once the "Feature Name" column was cross-referenced to the **MunicipalityName** column in the main dataset,
then the "ID" column was pasted into the main dataset and the column renamed to **GNIS_ID**.

## Colorado-Municipality-PointLocation.csv ##

This file is the saved attribute table of the
[Municipal Boundaries in Colorado](https://data.colorado.gov/Municipal/Municipal-Boundaries-in-Colorado/u943-ics6)
GeoJSON file downloaded from the Colorado Information Marketplace.
The GeoJSON file was opened in QGIS and the centroid of each municipality's
boundaries was calculated (the process is not described here).
The attribute table of the GeoJSON file was saved in CSV format.
**This process needs to be automated with the OWF GeoProcessor.**

The file contains the following data columns.

| **Column** | **Description** |
| -- | -- |
| **X** | Longitude of the point location of the municipality in decimal degrees; is the **Longitude** column in the main dataset. |
| **Y** | Latitude of the point location of the municipality in decimal degrees; is the **Latitude** column in the main dataset. |
| **first_city** | Name of the municipality; text format; original data column of the Municipal Boundaries in Colorado map; not used in main dataset. |
| **city** | Federal Information Processing Standard (FIPS) identifier; converted to text format to preserved leading zeroes; original data column of the Municipal Boundaries in Colorado map; manually cross-referenced to the **FIPS_ID** column in the main dataset. |
| **id** | Integer from 1 to 274; original data column of the Municipal Boundaries in Colorado map; not used in main dataset. |

Once the "city" column was cross-referenced to the **FIPS_ID** column in the main dataset,
then the "X" and "Y" columns were pasted into the main dataset and the columns renamed to **Longitude** and **Latitude**.

## Colorado-PWS-IDs.csv ##

This file contains original data downloaded from the EPA's
[Safe Drinking Water Information System](https://ofmpub.epa.gov/apex/sfdw/f?p=108:1:::NO:::)
containing Public Water System (PWS) IDs.
PWS IDs are useful for linking Environmental Protection Agency (EPA)
and Colorado Department of Public Health and Environment (CDPHE) datasets.
In addition, many municipalities and water providers publish "Consumer Confidence Reports"
or water quality reports on their websites and the PWS ID is listed on the report.
The ***Advanced Search Options*** was chosen after selecting Colorado as the ***Primacy Agency***.
Then the ***Water System Summary*** report option was selected.
Data were available for download in CSV format but must be manually downloaded.
The downloaded file was opened in Excel using the Get External Data From Text option to make sure identifiers are formatted properly.
The file was then renamed and saved again in CSV format.
**The number of records depends on when the report is generated.**

The file contains the following data columns.

| **Column** | **Description** |
| -- | -- |
| **PWS ID** | Public Water System identifier; text format; is the **PWS_ID** column in the main dataset. |
| **PWS Name** | name of the Public Water System; text format; manually cross-referenced to the **MunicipalityName** column in the main dataset. |
| **PWS Type** | type of Public Water System; options are community water system, non-transient non-community system or transient non-community system; text format; not used in main dataset. |
| **Primary Source** | source of water; options are surface water or ground water; text format; not used in main dataset. |
| **Counties Served** | county(s) within the PWS's service area, text format; already provided in the main dataset . |
| **Cities Served** | municipality(s) within the PWS's service area; text format; not used in main dataset. |
| **PopulationServed Count** | population served by the PWS; integer format; not used in the main dataset. |
| **Number of Facilities** | count of facilities associated with the PWS; can be water treatment facilities, storage tanks, etc.; integer format; not used in the main dataset. |
| **Number of Violations** | count of violations the PWS has received; integer format; not used in the main dataset. |
| **Number of Site Visits** | count of site visits to the PWS; integer format; not used in the main dataset. |

Once the "PWS Name" column was cross-referenced to the **MunicipalityName** column in the main dataset,
then the "PWS ID" column was pasted into the main dataset and the column renamed to **PWS_ID**.
