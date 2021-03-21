.. include:: ../html_lat.txt

Access to Copernicus satellite images for free
===============================================

Sentinel Hub EO Browser
------------------------
The `Sentinel Hub EO Browser <https://www.sentinel-hub.com/explore/eobrowser/>`_ (:numref:`Fig1_EObrowser`) is the first place to look for the archive of the European Space Agency’s `Sentinel-1 <https://sentinel.esa.int/web/sentinel/missions/sentinel-1>`_, `Sentinel-2 <https://sentinel.esa.int/web/sentinel/missions/sentinel-2>`_, `Sentinel-3 <https://sentinel.esa.int/web/sentinel/missions/sentinel-3>`_, `Sentinel-5P <https://sentinel.esa.int/web/sentinel/missions/sentinel-5p>`_, `PROBA-V <https://earth.esa.int/eogateway/missions/proba-v>`_, and `MERIS <https://earth.esa.int/eogateway/instruments/meris>`_ imagery. |br|
This repository also gives access to the images collected by NASA’s `Landsat-5 <https://landsat.gsfc.nasa.gov/landsat-4-5>`_, `Landsat-7 <https://landsat.gsfc.nasa.gov/landsat-7>`_, `Landsat-8 <https://landsat.gsfc.nasa.gov/landsat-8>`_, and `MODIS <https://modis.gsfc.nasa.gov/>`_ satellites, and even NASA’s `global imagery browse services (GIBS) <https://earthdata.nasa.gov/eosdis/science-system-description/eosdis-components/gibs>`_ products in one single place.

.. note:: **Registered users have access to more features!** |br|
	The `Sentinel Hub EO Browser <https://www.sentinel-hub.com/explore/eobrowser/>`_ also offers some basic tools to explore Earth observation data, develop custom scripts for simple image analysis and also use third-party scripts. |br|
	Before browsing the image archives, sign up for a `free account on Sentinel Hub EO Browser <https://apps.sentinel-hub.com/>`_ and then log in (:numref:`Fig2_EObrowser`).

.. _Fig1_EObrowser:
.. figure:: /img/3/Fig1_EObrowser.png
	:align: center

	Home page of the Sentinel Hub EO Browser.

|br|

.. _Fig2_EObrowser:
.. figure:: /img/3/Fig2_EObrowser.png
	:align: center

	Log in to the Sentinel Hub EO Browser.

|br|

.. _How-to-select-the-correct-products-with-Sentinel-Hub-EO-Browser:

How to select the correct products with Sentinel Hub EO Browser
````````````````````````````````````````````````````````````````
Once logged in the `Sentinel Hub EO Browser <https://www.sentinel-hub.com/explore/eobrowser/>`_, configure the search criteria (:numref:`Fig3_EObrowser`):

1. In this example, we look for Sentinel-2 images. Thus, select :guilabel:`Sentinel-2` as a data source,

2. Set :guilabel:`Advanced search` and select :guilabel:`L2A (atmospherically corrected)`. This option limits the search to atmospherically corrected Sentinel-2 images only,

3. Optionally, set the :guilabel:`Max. cloud coverage` to the desired level of maximum cloud cover accepted,

4. Select the starting and ending :guilabel:`Time range [UTC]` by clicking the calendars,

5. Optionally, select :guilabel:`filter by months` to limit the search to specific months in the time range,

6. Click the :guilabel:`Search` button to search the archive.

.. _Fig3_EObrowser:
.. figure:: /img/3/Fig3_EObrowser-2.png
	:align: center

	Set the searching criteria.

|br|

.. warning:: **Remember to use ONLY atmospherically corrected images!** |br|
	Multispectral satellite images capture both the sunlight reflected by the Earth’s surface and the light scattered by the atmosphere. However, when monitoring the environment, atmospheric scattering is a noise that must be removed before image manipulation or analysis. |br|
	Sentinel-2 data provided as ``L1C`` products are uncorrected images. Sentinel-2 data provided as ``L2A`` products are atmospherically corrected images. |br|
	**Only** ``L2A`` **products are ready for image processing!**

|br|

How to view the satellite images with Sentinel Hub EO Browser
````````````````````````````````````````````````````````````````
Select your image tile in the main window and click :guilabel:`Visualize`. Alternatively, you can load your image by clicking :guilabel:`Visualize` in the left panel (:numref:`Fig6_EObrowser`).

.. _Fig6_EObrowser:
.. figure:: /img/3/Fig6_EObrowser-2.png
	:align: center

	Select your satellite image archived in the Sentinel Hub EO Browser.

By default, `Sentinel Hub EO Browser <https://www.sentinel-hub.com/explore/eobrowser/>`_ opens a **true colour** image of the selected area (:numref:`Fig7_EObrowser`). For `Sentinel-2 <https://sentinel.esa.int/web/sentinel/missions/sentinel-2>`_, the Red, Green and Blue colours are recorded by spectral band 4, band 3, and band 2. Therefore, the Earth’s surface is shown as humans would see it naturally.

.. note:: **True colour synthesis:** |br|
	Satellite Red band → Image Red colour channel |br|
	Satellite Green band → Image Green colour channel |br|
	Satellite Blue band → Image Blue colour channel

.. _Fig7_EObrowser:
.. figure:: /img/3/Fig7_EObrowser.png
	:align: center

	The satellite image(s) are displayed.

However, `Sentinel Hub EO Browser <https://www.sentinel-hub.com/explore/eobrowser/>`_ shows the following additional pre-built colour composites:

**a. False colour** (:numref:`Fig8_EObrowser`). This is the well-know colour composite used to evaluate vegetation biomass and health. It uses the near infrared (NIR), Red, and Green spectral bands, represented as Red, Green and Blue colours respectively:

- Vegetation is from dark red to light red,
- Urban areas are cyan or tan,
- Bare soils are from dark brown to light brown,
- Water is black or dark blue,
- Snow and ice are cyan or blue,
- Clouds are white,
- Wildfires are white (the smoke plume).

.. note:: **False colour synthesis:** |br|
	Satellite NIR band → Image Red colour channel |br|
	Satellite Red band → Image Green colour channel |br|
	Satellite Green band → Image Blue colour channel

.. _Fig8_EObrowser:
.. figure:: /img/3/Fig8_EObrowser.png
	:align: center

	False colour composite.

|br|

**b. False colour (urban)** (:numref:`Fig15_EObrowser`). This colour composite is used to highlight details in the urbanized areas more clearly and spot wildfires. It uses two shortwave infrared (SWIR) spectral bands and the Red spectral bands, represented as Red, Green and Blue colours respectively:

- Vegetation is green,
- Urban areas are white, grey, or purple,
- Bare soils are shown in a variety of colours,
- Water is black or dark blue,
- Snow and ice are blue,
- Wildfires are red and yellow,
- Clouds qre white.

.. note:: **False colour (urban) synthesis:** |br|
	Satellite SWIR band 1 → Image Red colour channel |br|
	Satellite SWIR band 2 → Image Green colour channel |br|
	Satellite Red band → Image Blue colour channel

.. _Fig15_EObrowser:
.. figure:: /img/3/Fig15_EObrowser.png
	:align: center

	False colour (urban) composite.

|br|

**c. SWIR** (:numref:`Fig16_EObrowser`). This colour composite is used to distinguish between clouds, snow, and ice. Besides, it is useful for geological mapping. It uses a shortwave infrared (SWIR), a near infrared (NIR) and the red spectral bands, represented as red, green and blue colours respectively:

- Vegetation is green,
- Urban areas are brown,
- Bare soils are from dark brown to light brown,
- Water is black or dark blue,
- Snow and ice are blue,
- Clouds are white,
- Rocks are shown in a variety of colours.

.. note:: **SWIR colour synthesis:** |br|
	Satellite SWIR band → Image Red colour channel |br|
	Satellite NIR band → Image Green colour channel |br|
	Satellite Red band → Image Blue colour channel

.. _Fig16_EObrowser:
.. figure:: /img/3/Fig16_EObrowser.png
	:align: center

	Shortwave infrared (SWIR) composite.

|br|

`Sentinel Hub EO Browser <https://www.sentinel-hub.com/explore/eobrowser/>`_ also shows the maps of some basic spectral indices. These parameters are useful to recognize different land cover types and monitor the status of vegetated land. Specifically:

**a. NDVI** (:numref:`Fig9_EObrowser`). The *Normalized Difference Vegetation Index (NDVI)* is the basic greenness vegetation index used to estimate biomass and health of the green vegetation. The index is calculated using a combination of the near infrared (NIR) and red spectral bands (see :ref:`Normalized Difference Vegetation Index (NDVI) <Normalized-Difference-Vegetation-Index>`):

.. math:: NDVI=\frac{\rho_{NIR}-\rho_{Red}}{\rho_{NIR}+\rho_{Red}}

.. _Fig9_EObrowser:
.. figure:: /img/3/Fig9_EObrowser.png
	:align: center

	Map of the Normalized Difference Vegetation Index (NDVI).

|br|

**b. Moisture index** (:numref:`Fig17_EObrowser`). The *Normalized Difference Moisture Index (NDMI)* is used to estimate vegetation water content and monitor droughts. The index is calculated using a combination of the near infrared (NIR) and shortwave infrared (SWIR) spectral bands:

.. math:: NDMI=\frac{\rho_{NIR}-\rho_{SWIR}}{\rho_{NIR}+\rho_{SWIR}}

.. note:: The Normalized Difference Moisture Index (NDMI) is also referred as Normalized Difference Water Index (NDWI) (see :ref:`Normalized Difference Water Index (NDWI) <Normalized_Difference_Water_Index2>`).

.. _Fig17_EObrowser:
.. figure:: /img/3/Fig17_EObrowser.png
	:align: center

	Map of the Normalized Difference Moisture Index (NDMI).

|br|

**c. NDWI** (:numref:`Fig18_EObrowser`). The *Normalized Difference Water Index (NDWI)* is used to map water bodies. The index is calculated using a combination of the near infrared (NIR) and green spectral bands (see :ref:`Normalized Difference Water Index (NDWI) <Normalized_Difference_Water_Index1>`):

.. math:: NDWI=\frac{\rho_{Green}-\rho_{NIR}}{\rho_{Green}+\rho_{NIR}}

.. _Fig18_EObrowser:
.. figure:: /img/3/Fig18_EObrowser.png
	:align: center

	Map of the Normalized Difference Water Index (NDWI).

|br|

**d. NDSI** (:numref:`Fig19_EObrowser`). The *Normalised Difference Snow Index (NDSI)* is used to map clouds and snow. The index is calculated using a combination of the shortwave infrared (SWIR) and green spectral bands (see :ref:`Normalized Difference Snow Index (NDSI) <Normalized_Difference_Snow_Index>`):

.. math:: NDSI=\frac{\rho_{Green}-\rho_{SWIR}}{\rho_{Green}+\rho_{SWIR}}

.. _Fig19_EObrowser:
.. figure:: /img/3/Fig19_EObrowser.png
	:align: center

	Map of the Normalised Difference Snow Index (NDSI).

|br|

Additionally, there is a simple scene classification map with the following classes (:numref:`Fig10_EObrowser`):

- Vegetation,
- Not-vegetated,
- Water,
- Snow or ice,
- Clouds

	- (medium probability of) Cloud,
	- (high probability of) Cloud,
	- Thin cirrus (i.e. cloud),

- Shadows

	- Dark features and shadows,
	- Cloud shadows,

- Missing data

	- No data,
	- Saturated or defective pixel. 

.. _Fig10_EObrowser:
.. figure:: /img/3/Fig10_EObrowser.png
	:align: center

	Scene classification map.

|br|

.. hint:: **Looking for a specific spectral index?** |br|
	The `Index DataBase <https://www.indexdatabase.de/>`_ is a collection of spectral indices for different applications and sensors. Here you find a selection of `250 spectral indices designed to fit the images of the Sentinel-2 satellite <https://www.indexdatabase.de/db/is.php?sensor_id=96>`_. |br|

	**If you like to import these spectral indices into Sentinel Hub EO Browser, try these** `javascripts <https://custom-scripts.sentinel-hub.com/custom-scripts/sentinel-2/indexdb/>`_.

|br|

How to download the data with Sentinel Hub EO Browser
````````````````````````````````````````````````````````
.. warning:: **Sign up for Copernicus Open Access Hub.** |br|
	The images searched with `Sentinel Hub EO Browser <https://www.sentinel-hub.com/explore/eobrowser/>`_ are downloaded from the `Copernicus Open Access Hub <https://scihub.copernicus.eu/dhus/#/home>`_. `Sign up for a free account! <https://scihub.copernicus.eu/dhus/#/home>`_

|br|

1. Click the green chain symbol to show the download link at the bottom of the image (:guilabel:`SciHub link:`),

2. Click the link to download the data.

.. _Fig14_EObrowser:
.. figure:: /img/3/Fig14_EObrowser.png
	:align: center

	Activate the link to download the images.

3. If you are already logged in the `Copernicus Open Access Hub <https://scihub.copernicus.eu/dhus/#/home>`_, the download starts immediately. Otherwise, you will be prompted for user name and password of `Copernicus Open Access Hub <https://scihub.copernicus.eu/dhus/#/home>`_.

.. caution:: Username & password for `Sentinel Hub EO Browser <https://www.sentinel-hub.com/explore/eobrowser/>`_ are different from that of `Copernicus Open Access Hub <https://scihub.copernicus.eu/dhus/#/home>`_!

|br|

.. seealso:: For additional information, see the `Sentinel Hub EO Browser user guide <https://www.sentinel-hub.com/explore/eobrowser/user-guide/>`_

|br|
|br|

Some alternative repositories
------------------------------
Alternative European repositories are the Copernicus Open Access Hub (:numref:`Fig1_scihub`) and the DIASs (:numref:`Fig_DIAS`) listed below. However, they are usually more complex than Sentinel Hub EO Browser. They might also have a different level of maturity, data archived and user-friendliness. |br|
Discover more information on the `Copernicus Open Access Hub <https://scihub.copernicus.eu/dhus/#/home>`_ and on the five `Data and Information Access Services (DIAS) <https://www.copernicus.eu/en/access-data/dias>`_:

- `CREO DIAS <https://creodias.eu>`_,
- `MUNDI web services <https://mundiwebservices.com>`_,
- `ONDA DIAS <https://www.onda-dias.eu/cms>`_,
- `Sobloo <https://sobloo.eu>`_,
- `WEkEO <https://wekeo.eu>`_.

.. _Fig1_scihub:
.. figure:: /img/3/Fig1_scihub.png
	:align: center

	Copernicus Open Access Hub.

.. _Fig_DIAS:
.. figure:: /img/3/Fig_DIAS.png
	:align: center

	Data and Information Access Services (credit: European Commission).

.. caution:: Sentinel images could also be downloaded from the US repositories `EarthExplorer <https://earthexplorer.usgs.gov/>`_ and `GloVis <https://glovis.usgs.gov/app?fullscreen=0>`_. However, this repository mirrors only ``L1C`` products (i.e. images which are NOT atmospherically corrected)!

|br|
|br|

(v.2103211807)