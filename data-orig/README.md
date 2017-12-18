# data-orig folder #

The data-orig folder contains original data files downloaded from various agency websites.  The contents of each file are described below, as well as the methodology used to obtain the data.

## Colorado-DOLA-LocalGovt-IDs-Municipality.csv ##

This file is a copy of the Department of Local Affairs (DOLA)'s [Local Government Information System](https://dola.colorado.gov/lgis/municipalities.jsf) website that contains local government IDs (DOLA_LG_ID).  These data are not available in a machine-readable, downloadable format.  Therefore, the data were copied directly from the website and pasted into Excel.  It was necessary to convert LG IDs to text to preserve leading zeroes.  IDs with leading zeroes needed to have those zeroes added back in to make sure that the LG ID is a 5-digit number.  
The file was then saved in CSV format.
**OWF is working on a process to automatically download DOLA_LG_IDs within TSTool.  This will allow for easier processing of data and to check if any updates have been made to the dataset.  So far, efforts through the State Demography Office and the Colorado Information Marketplace have not been successful.  OWF believes there may be an error in the files.**  

The file contains the following data columns.

* **City/Town Name:** -- name of the municipality
* **Type:** -- type of municipality
* **LG ID:** -- 5-digit identifier used by DOLA
* **FIPS:** -- 5-digit [Federal Information Processing Standard](https://www.census.gov/geo/reference/codes/place.html) code
* **Census MRF:** -- census master reference file 
* **Counties:** -- county(s) in which the municipality is contained


## Colorado-FIPS-Places.csv ##

This file contains original data downloaded from the [U.S.Census Bureau](https://www.census.gov/geo/reference/codes/place.html) containing Federal Information Processing Standard (FIPS) IDs.
Data are available as pipe-delimited files.  The file was then saved in CSV format.
**OWF is working on a process to automatically download FIPS IDs within TSTool.  This will allow for easier processing of data and to check if any updates have been made to the dataset.  One problem with the data is that the pipe-delimited file does not contain column headings, which makes it difficult to use within TSTool.**

The file contains the following data columns.  Note that the data column names are not currently listed in the file.  Column names can be found [here](https://www.census.gov/geo/reference/codes/place.html).

* **STATE** -- 2-letter state postal code
* **STATEFP** -- 2-digit state FIPS code
* **PLACEFP** -- place or county subdivision FIPS code
* **PLACENAME** -- place or county subdivision name and legal/statistical area description
* **TYPE** -- type of place or county subdivision
* **FUNCSTAT** -- functional status; see website
* **COUNTY** -- county(s) in which the place or county subdivision is located


## Colorado-GNIS-Civil.csv ##

This file contains original data downloaded from the [Geographic Names Information System (GNIS)](https://geonames.usgs.gov/apex/f?p=138:2:0::NO:RP::) containing GNIS IDs.
Data are available as pipe-delimited files.  The file was then saved in CSV format.
**OWF is working on a process to automatically download GNIS IDs within TSTool.  This will allow for easier processing of data and to check if any updates have been made to the dataset.**

The file contains the following data columns.

* **Feature Name** -- name of either the municipality, county or division, with the words "County", "Division", "Town of" or "City of" contained in the name
* **ID** -- GNIS ID
* **Class** -- class of the feature; note that all are "Civil"
* **County** -- county(s) in which the municipality is contained
* **State** -- state the feature is located in
* **Latitude** -- latitude in degrees-minutes-seconds
* **Longitude** -- longitude in degrees-minutes-seconds
* **Ele(ft)** -- elevation of the feature, in feet
* **Map** -- USGS topographic map name
* **BGN Date** -- Board of Geographic Names date
* **Entry Date** -- date entered into the system


## Colorado-Municipality-PointLocation.csv ##

This file is the saved attribute table of the [Municipal Boundaries in Colorado](https://data.colorado.gov/Municipal/Municipal-Boundaries-in-Colorado/u943-ics6) geojson file downloaded from the Colorado Information Marketplace.  The geojson file was opened in QGIS and the centroid of each municipality's boundaries was calculated (the process is not described here).  
The attribute table of the geojson file was saved in CSV format.

The file contains the following data columns.

* **X** -- longitude of the point location of the municipality in decimal degrees.
* **Y** -- latitude of the point location of the municipality in decimal degrees.
* **first_city** -- name of the municipality; original data column of the Municipal Boundaries in Colorado map
* **city** -- Federal Information Processing Standard (FIPS) identifier; original data column of the Municipal Boundaries in Colorado map
* **id** -- integer from 1 to 274; original data column of the Municipal Boundaries in Colorado map


## Colorado-PWS-IDs.csv ##

This file contains original data downloaded from the EPA's [Safe Drinking Water Information System](https://ofmpub.epa.gov/apex/sfdw/f?p=108:1:::NO:::) containing Public Water System (PWS) IDs.
The Advanced Search Options was chosen after selecting Colorado as the Primacy Agency.  Then the Water System Summary report option was selected.  Data were available for download in CSV format.
**OWF is working on a process to automatically download PWS IDs within TSTool.  This will allow for easier processing of data and to check if any updates have been made to the dataset.**

The file contains the following data columns.

* **PWS ID** -- Public Water System identifier
* **PWS Name** -- name of the Public Water System
* **PWS Type** -- type of Public Water System; options are community water system, non-transient non-community system or transient non-community system
* **Primary Source** -- source of water; options are surface water or ground water
* **Counties Served** -- county(s) within the PWS's service area
* **Cities Served** -- municipality(s) within the PWS's service area
* **PopulationServed Count** -- population served by the PWS
* **Number of Facilities** -- count of facilities associated with the PWS; can be water treatment facilities, storage tanks, etc.
* **Number of Violations** -- count of violations the PWS has received
* **Number of Site Visits** -- count of site visits to the PWS
