.. include:: ../html_lat.txt

.. _Fundamentals-of-remote-sensing-and-Earth-observation:

Fundamentals of multispectral Earth observation
===============================================

Remote sensing, Earth observation and GIS
-----------------------------------------
Remote sensing and Earth observation are often used interchangeably, but they refer to different concepts:

**Remote sensing** is the

	*"The gathering of information without actual physical contact with what is being observed. This involves the use of radars, sonars, spectroscopy, and the use of airborne and satellite photography."*  |br|
	(Credit: `Oxford Dictionary of Earth Sciences. © Oxford University Press <https://www.oxfordreference.com/view/10.1093/oi/authority.20110803100413590>`_).

while **Earth observation** (EO) is the

	*"The gathering of information about planet Earth’s physical, chemical and biological systems via remote sensing technologies, usually involving satellites carrying imaging devices. Earth observation is used to monitor and assess the status of, and changes in, the natural and manmade environment."*  |br|
	(Credit: `European Commission <https://ec.europa.eu/jrc/en/research-topic/earth-observation>`_).

That means *Earth observation* **is the process** of collecting information on our planet using **contactless** *remote sensing* **technologies**.

We already know (see :ref:`1.1`) that a **geographic information system (GIS)** is an:

	*"Integrated system of computer hardware, software, and trained personnel linking topographic, demographic, utility, facility, image and other resource data that is geographically referenced."* |br| 
	(Credit: `NASA <https://www.nasa.gov/>`_).

Thus, *Earth observation* provides **data** collected with *remote sensing* **systems** and a set of methods for their **processing** and **analysis**, while *geographic information systems* offer a framework for the **management**, **manipulation**, **query** and **representation** of the geospatial information.

|br|
|br|

Satellites for Earth observation
---------------------------------
Today, hundreds of satellites are orbiting or planet. They differ for:

- Orbits and revisit time,
- Imaging cameras,
- Spatial resolution and swath width,
- Spectral characteristics,

All these characteristics are defined during the mission design, depending on the satellite mission’s specific applications.

For example, to monitor the weather at a global scale and in real-time, we need satellites with a very high orbit, a low spatial resolution with a large swath, and a few spectral bands (:numref:`Fig_Meteo_SAT`).

.. _Fig_Meteo_SAT:
.. figure:: /img/3/Fig0_SAT.png
	:align: center

	Earth observation missions developed by the European Space Agency (credit: EUMETSAT [2021] – CC BY-SA IGO 3.0).

.. hint:: Click here to see `real-time meteo imageries over Europe <https://view.eumetsat.int/productviewer?v=default>`_ *(Credit: EUMETSAT – CC BY-SA IGO 3.0).*

On the opposite, to monitor our urban areas, we need satellites with a low orbit, a high spatial resolution with a small swath, and many spectral bands (:numref:`Fig_30cm_SAT`).

.. _Fig_30cm_SAT:
.. figure:: /img/3/Fig00_SAT.png
	:align: center

	Earth observation missions developed by the European Space Agency (credit: © European Space Imaging).

.. hint:: Click here to see `a 30 cm satellite image over Madrid (Spain) <https://www.euspaceimaging.com/30-cm/>`_  *(Credit: © European Space Imaging).*

.. .. _Fig_intro_SAT:
.. .. figure:: /img/3/Fig_intro_SAT.png
	:align: center

.. 	Earth observation missions developed by the European Space Agency (credit: ESA – CC BY-SA IGO 3.0).

|br|

Satellite orbits and revisit time
````````````````````````````````````
**a. Geostationary orbit (GEO)** |br|
Satellites in geostationary orbit circle Earth above the equator from west to east following Earth’s rotation at an *altitude of 35,800 km* and a *speed of about 3 km/s*. This makes geostationary satellites to be ‘stationary’ over a fixed location. |br|
These satellites can image the portion of the Earth's surface they are looking at every 30 minutes or less. **Most of the satellites used for weather forecasts have a geostationary orbit.**

**b. Medium Earth orbit (MEO)** |br|
Satellites in a medium Earth orbit circle the Earth at an *altitude between 1,000 km and 35,800 km*, with *revisit times defined by their orbital altitude*. |br|
Satellites for Earth observation do not use this orbit. However **navigation satellites, like the European Galileo system or the American GPS, have a medium Earth orbit.**

**c. Low Earth orbit (LEO)** |br|
Satellites in a low Earth orbit circle close to Earth’s surface, at an *altitude between 200 km and 1,000 km* and a *speed of about 7.8 km/s*. At this speed, a satellite takes approximately 90 minutes to circle Earth. Thus, travels around Earth about 16 times a day.

**d. Sun-synchronous orbit (SSO)** |br|
This is a particular kind of Low Earth Orbit, where satellites circle from north to south and are always in the same ‘fixed’ position relative to the Sun. This means that the satellites still visits the same geographic location at the same local time. |br|
**Most of satellites for Earth observation have a Sun-synchronous low Earth orbit, with an altitude between 600 km and 800 km and a speed of approximately 7.5 km/s.**

.. note:: Depending on the time for revisiting the same geographic location, satellites are classified as:

	- **High revisit time:** < 3 days
	- **Medium revisit time:** 4 - 16 days
	- **Low revisit time:** > 16 days

.. _Fig1_SAT:
.. figure:: /img/3/Fig1_SAT.png
	:align: center

	Satellite orbits (credit: adapted from Mark Mercer, 2011 - CC BY-SA 4.0).

.. hint:: **Small activity** |br|
	See the real-time location of about 19,300 manmade objects orbiting the Earth with `ESRI Satellite Map <https://maps.esri.com/rc/sat2/index.html#>`_ (updated on 14 July 2020).

.. hint:: **Small activity** |br|
	Search for a specific satellite with the `live real time satellite tracking and predictions <https://www.n2yo.com/>`_ (up to date).

|br|

Digital images and the EM spectrum
````````````````````````````````````
A greyscale digital image is a **matrix** (i.e. table) of individual elements (called **pixels**) representing the **brightness** of a specific geographic location recorded in a particular **range of wavelengths of the electromagnetic spectrum** (called **spectral band**, or just **band**) (:numref:`Fig3_SAT`).

.. _Fig3_SAT:
.. figure:: /img/3/Fig3_SAT.png
	:align: center

	The digital image as a table of numbers.

**But what are the electromagnetic spectrum and wavelengths?** |br|
Consider the electromagnetic spectrum as the full range of “light” that exists in the universe (:numref:`Fig4_SAT`): from Gamma rays (shorter wavelengths) to Radio waves (longer wavelengths). |br|
We can think of the different wavelengths as different “colours”.

.. _Fig4_SAT:
.. figure:: /img/3/Fig4_SAT.png
	:align: center

	The electromagnetic spectrum (credit: NASA – CC BY-SA 3.0).

Unfortunately, most of these “colours” and “light” are invisible to our eyes! |br|
We humans can see only the colours of the **VISIBLE** light. However, many other “colours” exists, and some animals can see them. For instance, snakes can sense the INFRARED (i.e. the heat) and some insects can see the ULTRAVIOLET. |br|
:numref:`Fig5_SAT` and :numref:`Fig6_SAT` show how human eyes and animal eyes sense different wavelengths of the electromagnetic spectrum.

.. _Fig5_SAT:
.. figure:: /img/3/Fig5_SAT.png
	:align: center

	The electromagnetic spectrum sensed by humans, cats and snakes.

.. _Fig6_SAT:
.. figure:: /img/3/Fig6_SAT.png
	:align: center

	The electromagnetic spectrum sensed humans and bees.

.. hint:: **< Small activity >** |br|
	See planet Earth live from the International Space Station with the `External High Definition Camera <https://www.n2yo.com/space-station/>`_ (real time streaming).

|br|

.. _Spectral-characteristics:

Spectral characteristics
`````````````````````````
Optical satellites use special “cameras”, called **multispectral cameras** (:numref:`Fig_camera_SAT`).

.. _Fig_camera_SAT:
.. figure:: /img/3/Fig_camera_SAT.png
	:align: center

	The imaging camera of the Sentinel-2 satellite (credit: ESA – CC BY-SA IGO 3.0).

Multispectral cameras produce multispectral (=multiband) grayscale images. That is to say, a multitude of greyscale images - *collected at the same time* - recording the reflected sunlight in a specific range of wavelengths (i.e. the spectral bands) (:numref:`Fig7_SAT`). |br|
**In other words, a multiband image describes the intensity of the different “colours” sensed in the different “lights” of the electromagnetic spectrum** (also see :ref:`1.3.1`).

.. _Fig7_SAT:
.. figure:: /img/3/Fig7_SAT.png
	:align: center

	Example of multiband image.

.. note:: In photography, spectral bands are usually called **colour channels**. |br|
	A smartphone takes pictures in only 3 VISIBLE colour channels:

	- Blue channel,
	- Green channel,
	- Red channel.
	
	But satellites allow extending our visual perception to many more “colours”, even to wavelengths  where our eyes are blind!

.. hint:: **Small activity** |br|
	To see the colour channels, try `RGB channels splitter <https://www.dcode.fr/rgb-channels>`_ with a photo taken with your smartphone (:numref:`Fig8_SAT`)! Try using both outputs "as greyscale", and "with their own colour". |br|
	You might also use this `test picture <https://drive.google.com/file/d/1B5RIfx63mQq3O908Etstn5zeHTKBkPQu/view?usp=sharing>`_.

.. _Fig8_SAT:
.. figure:: /img/3/Fig8_SAT.png
	:align: center

	Colour channels splitter.

The combination of different greyscale spectral bands produces the colours of satellite images (:numref:`Fig_Venezia_SAT`).

.. _Fig_Venezia_SAT:
.. figure:: /img/3/Fig_Venezia_SAT.png
	:align: center

	Satellite colour image of Venice (Italy). Contains Copernicus Sentinel data.

.. hint:: **Small activity** |br|
	Try the `Remote Sensing Virtual Lab <https://remotesensinglab.com/visualising.html>`_ to see how the land looks like in different wavelengths (cretits: Karen Joyce).

.. hint:: **Small activity** |br|
	Try `Combine RGB channels <http://flaticon.sodhanalibrary.com/combine-rgb-chanels-online.html>`_ to combine greyscale satellite images into a satellite colour image:

	- Download Sentinel-2 image of Venice `(Blue band) <https://drive.google.com/file/d/10rNhnS-okkBZekTnDR5CDjcZ9PztkADW/view?usp=sharing>`_,
	- Download Sentinel-2 image of Venice `(Green band) <https://drive.google.com/file/d/1SakQNI3DDrisNKqoh1jfjxD5ffA31HQN/view?usp=sharing>`_,
	- Download Sentinel-2 image of Venice `(Red band) <https://drive.google.com/file/d/1UWXjSDw-UZCC5nERktAOBFO-pst2buzM/view?usp=sharing>`_,

	*What happens to colours if you mix up the bands?*

|br|

Spatial resolution and swath width
````````````````````````````````````
The spatial resolution specifies the pixel size of satellite images at the Earth surface. It describes the ability to separate small spatial details. |br|
Depending on their image pixel size, remote sensing cameras are classified as:

- **Very high spatial resolution:** < 1 m,
- **High spatial resolution:** 1 -5 m,
- **Medium spatial resolution:** 5 - 100 m,
- **Low spatial resolution:** > 100 m.

The area imaged on the surface is called **swath**. Thus, the swath defines the geographic extent of a single satellite image. |br|
Generally speaking:

- **Low resolution** imaging cameras have a **large swath**: up to thousands of km,
- **Very high resolution** imaging cameras have a **small swath**: about dozen of km.

.. _Fig2_SAT:
.. figure:: /img/3/Fig2_SAT.png
	:align: center

	The London Eye (UK). The effect of spatial resolution on image detail and swath.

Very high resolution cameras are typically needed for applications requiring great spatial detail of a particular site, such as mapping buildings damaged by an earthquake. Such cameras would generally be onboard of a Low Earth Orbit satellite and have a narrow swath. In such an orbit, images can only be acquired when the satellite passes over the area of interest.

On the opposite, Geostationary satellites have low resolution cameras with wide swath. In such an orbit, images over the area of interest are acquired continuously. These satellites are suitable for continental and global studies.

*Medium resolution cameras with pixel size between 10 m and 30 m usually have a swath of about 200-300 km. They are often a good compromise for many application needs.*

.. tip:: **Spatial resolution vs orbital altitude** |br|
	The spatial resolution is proportional to the orbital altitude. Thus, Geostationary satellites have a low spatial resolution, while Low Earth Orbit satellites could achieve very high spatial resolution.

|br|
|br|

Copernicus and the Sentinels
-----------------------------

The Copernicus programme
`````````````````````````
`Copernicus <https://www.copernicus.eu>`_ is the flagship European Union’s Earth Observation Programme, looking at our planet and its environment. Every day, Copernicus collects a large amount of global data from ground stations, satellites, airborne and seaborne systems. Then, transforms these data into information to support public authorities, international organisations and the industry in improving the quality of life for all European citizens.

Copernicus’s information can be used by end-users for a wide range of applications and various subject areas, including:

- Urban area management,
- Sustainable development and nature protection,
- Regional and local planning,
- Agriculture,
- Forestry,
- Fisheries,
- Health,
- Civil protection,
- Infrastructure,
- Transport and mobility,
- Tourism.

|br|

.. _Multispectral-Sentinel-satellites:

.. _3.1.3.2:

Multispectral Sentinel satellites
````````````````````````````````````
**Sentinel-2** |br|
The Sentinel-2 satellites (twin satellites Sentinel-2A and Sentinel-2B) provide **multispectral medium resolution imagery** for land services. |br|
Their orbit is Sun-synchronous, and the constellation (2 identical satellites) has an overall revisit time of 5 days at the equator and about 2-3 days at mid-latitudes. |br|

The mission objectives for Sentinel-2 are systematic:

- Land observation of vegetation and soil and water cover, inland waterways and coastal areas,
- Land use and change detection maps,
- Providing support in generating land cover,
- Disaster relief support,
- Climate change monitoring.

.. _Tab1_S2:
.. table:: Sentinel-2 spectral bands.

   ====  ==========================  ==================  ===========  ===========================================================================
   Band  "Light" (colour)            Spatial resolution  Swath width  Application
   ====  ==========================  ==================  ===========  ===========================================================================
   1     Visible (Violet)            60 m                290 km       Estimation of atmospheric aerosol
   2     Visible (Blue)              10 m                290 km       Mapping reflected Blue light
   3     Visible (Green)             10 m                290 km       Mapping reflected Green light
   4     Visible (Red)               10 m                290 km       Mapping reflected Red light
   5     Near infrared 1 (red edge)  20 m                290 km       Classification of vegetation
   6     Near infrared 2 (red edge)  20 m                290 km       Classification of vegetation
   7     Near infrared 3 (red edge)  20 m                290 km       Classification of vegetation
   8     Near infrared 4             10 m                290 km       Sensitive to chlorophyll and biomass
   8A    Near infrared 5 (red edge)  20 m                290 km       Classification of vegetation
   9     Near infrared 6             60 m                290 km       Estimation of atmospheric water vapor
   10    Short-wave infrared 1       60 m                290 km       Detection of clouds (cirrus)
   11    Short-wave infrared 2       20 m                290 km       Sensitive to lignin, discrimination of snow / ice / clouds
   12    Short-wave infrared 3       20 m                290 km       Distinction of live and dead biomass, discrimination of snow / ice / clouds
   ====  ==========================  ==================  ===========  ===========================================================================

.. hint:: See how Sentinel-2 `collects multispectral images <https://www.esa.int/ESA_Multimedia/Videos/2016/08/Sentinel-2_s_multispectral_imager_in_action>`_

|br|

**Sentinel-3** |br|
The Sentinel-3 satellites (twin satellites Sentinel-3A and Sentinel-3B) provide **multispectral low resolution imagery** for ocean and land services. |br|
Their orbit is Sun-synchronous, and the constellation (2 identical satellites) has an overall revisit time of fewer than 2 days. |br|

The *Ocean and Land Colour Instrument (OLCI)* has a 300-meters spatial resolution in 21 spectral bands, with a swath width of 1,270 km. |br|
The *Sea and Land Surface Temperature Radiometer (SLSTR)* instrument record the surface temperature with 1 km spatial resolution.

The mission objectives for Sentinel-3 are global coverage of:

- Ocean and land-surface temperature,
- Ocean and land-surface colour,
- Sea-water quality and pollution monitoring,
- Inland water monitoring, including rivers and lakes,
- Aid ocean forecasts with acquired data,
- Climate monitoring and modelling,
- Land-use change monitoring,
- Forest cover mapping,
- Fire detection,
- Weather forecasting,
- Measuring Earth’s thermal radiation for atmospheric applications.

.. _Tab1_S3:
.. table:: Sentinel-3 OLCI spectral bands.

   ====  ==========================  ==================  ===========  ===========================================================
   Band  "Light" (colour)            Spatial resolution  Swath width  Application
   ====  ==========================  ==================  ===========  ===========================================================
   1     Visible 1 (Violet)          300 m               1,270 km     Aerosol correction, improved water constituent retrieval
   2     Visible 2 (Violet)          300 m               1,270 km     Yellow substance and detrital pigments (turbidity)
   3     Visible 3 (Violet-Blue)     300 m               1,270 km     Chlorophyll absorption maximum, biogeochemistry, vegetation
   4     Visible 4 (Cyan)            300 m               1,270 km     High Chlorophyll
   5     Visible 5 (Green)           300 m               1,270 km     Chlorophyll, sediment, turbidity, red tide
   6     Visible 6 (Green)           300 m               1,270 km     Chlorophyll reference (Chlorophyll minimum)
   7     Visible 7 (Red)             300 m               1,270 km     Sediment loading
   8     Visible 8 (Red)             300 m               1,270 km     Chlorophyll, sediment, yellow substance/vegetation
   9     Visible 9 (Red)             300 m               1,270 km     Improved fluorescence retrieval
   10    Visible 10 (Red)            300 m               1,270 km     Chlorophyll fluorescence peak
   11    Near infrared 1 (red edge)  300 m               1,270 km     Chlorophyll fluorescence baseline
   12    Near infrared 2 (red edge)  300 m               1,270 km     Oxigen absorption, clouds, vegetation
   13    Near infrared 3 (red edge)  300 m               1,270 km     Aerosol correction
   14    Near infrared 4 (red edge)  300 m               1,270 km     Atmospheric correction
   15    Near infrared 5 (red edge)  300 m               1,270 km     Fluorescence over land
   16    Near infrared 6 (red edge)  300 m               1,270 km     Atmospheric/aerosol correction
   17    Near infrared 7             300 m               1,270 km     Atmospheric/aerosol correction, clouds
   18    Near infrared 8             300 m               1,270 km     Water vapour absorption, vegetation monitoring
   19    Near infrared 9             300 m               1,270 km     Water vapour absorption, vegetation monitoring
   20    Near infrared 10            300 m               1,270 km     Water vapour absorption, atmospheric correction
   21    Near infrared 11            300 m               1,270 km     Atmospheric/aerosol correction
   ====  ==========================  ==================  ===========  ===========================================================

.. _Tab1_S4:
.. table:: Sentinel-3 SLSTR spectral bands.

   ====  =====================  ==================  ===========  ===============================================
   Band  "Light" (colour)       Spatial resolution  Swath width  Application
   ====  =====================  ==================  ===========  ===============================================
   S1    Visible 1 (Green)      500 m               1,270 km     Cloud screening, vegetation monitoring, aerosol
   S2    Visible 2 (Red)        500 m               1,270 km     Vegetation monitoring, aerosol
   S3    Near infrared          500 m               1,270 km     Cloud
   S4    Short-wave infrared 1  500 m               1,270 km     Cirrus detection over land
   S5    Short-wave infrared 2  500 m               1,270 km     Cloud, ice, snow, vegetation monitoring
   S6    Short-wave infrared 3  500 m               1,270 km     Vegetation state and clouds
   S7    Thermal infrared 1     1 km                1,270 km     Active fires
   S8    Thermal infrared 2     1 km                1,270 km     Surface temperature, active fires
   S9    Thermal infrared 3     1 km                1,270 km     Surface temperature
   F1    Thermal infrared 4     1 km                1,270 km     Active fires
   F2    Thermal infrared 5     1 km                1,270 km     Surface temperature, active fires
   ====  =====================  ==================  ===========  ===============================================

.. hint:: `Look inside Sentinel-3 <http://www.esa.int/ESA_Multimedia/Videos/2016/01/A_multitalented_mission>`_

.. raw:: html

	<iframe src="https://www.esa.int/content/view/embedjw/463803" width="640" height="360" frameborder="0"></iframe>

*(Credit: ESA/ATG medialab – CC BY-SA IGO 3.0).*

|br|

**Sentinel-5P** |br|
Sentinel-5P is the precursor mission of Sentinel-5 and provides **multispectral extremely low resolution imagery** for atmospheric and climate services. |br|

The mission objective for Sentinel-5P is to provide daily global information on air pollutants for the atmosphere monitoring and climate change services:

	- Aerosols,
	- Clouds,
	- Ozone :math:`(O_3)`,
	- Nitrogen dioxide :math:`({\rm NO}_2)`,
	- Carbon monoxide :math:`(CO)`,
	- Sulfur dioxide :math:`({\rm SO}_2)`,
	- Methane :math:`({\rm CH}_4)`,
	- Formaldehyde :math:`({\rm CH}_2O)`.

.. _Tab1_S5:
.. table:: Sentinel-5P spectral bands.

   ====  ==============================  ==================  ===========
   Band  "Light" (colour)                Spatial resolution  Swath width
   ====  ==============================  ==================  ===========
   1     Ultraviolet 1                   28 km x 7 km        2,670 km
   2     Ultraviolet 2                   3.5 km x 7 km       2,670 km
   3     Ultraviolet & Visible (Violet)  3.5 km x 7 km       2,670 km
   4     Visible (Violet-Blue)           3.5 km x 7 km       2,670 km
   5     Near Infrared 1                 3.5 km x 7 km       2,670 km
   6     Near Infrared 2                 3.5 km x 7 km       2,670 km
   7     Short-wave infrared 1           7 km x 7 km         2,670 km
   8     Short-wave infrared 2           7 km x 7 km         2,670 km
   ====  ==============================  ==================  ===========

.. hint:: **Small activity** |br|
	See the benefits of the lockdown in China `on air quality <https://www.esa.int/Applications/Observing_the_Earth/Copernicus/Sentinel-5P/COVID-19_nitrogen_dioxide_over_China>`_

.. seealso:: For additional information, `discover all the Sentinel satellites <https://www.copernicus.eu/en/about-copernicus/infrastructure/discover-our-satellites>`_

|br|
|br|

Beyond satellite images
------------------------
Copernicus is not only satellite images. It also collects information from many sensors on the ground, sea, and air and transforms all these data into useful information to monitor changes and create forecasts.

These value-added products are delivered to users through the six thematic Copernicus services:

- Atmosphere,
- Marine,
- Land,
- Climate change,
- Security,
- Emergency,

|br|

Copernicus Atmosphere Monitoring Service
`````````````````````````````````````````
The `Copernicus Atmosphere Monitoring Service <https://atmosphere.copernicus.eu/>`_ provides data and information on atmospheric composition. It describes the current situation, forecasts a few days ahead, and analyses consistently retrospective data records for recent years. 

For example, the Copernicus Atmosphere Monitoring Service provides daily information on the global atmospheric composition by monitoring and forecasting constituents such as greenhouse gases, reactive gases, ozone and aerosols. The service also delivers information on the solar radiation at the Earth’s surface (which is essential for health, agriculture and renewable energies), near-real-time analysis, 4-day forecasts, and reanalysis of the European air quality.

Overall, the service focuses on five main areas:

- Air quality and atmospheric composition,
- Ozone layer and ultra-violet radiation,
- Emissions and surface fluxes,
- Solar radiation,
- Climate forcing.

.. hint:: **Small activity** |br|
	See `today’s air quality forecasts in Europe <http://macc-raq-op.meteo.fr/index.php?category=ensemble&subensemble=hourly_ensemble&date=LAST&calculation-model=ENSEMBLE&species=o3&level=SFC&offset=000>`_.

.. seealso:: For additional information, see the `Copernicus Atmosphere Monitoring Service web site <https://atmosphere.copernicus.eu/>`_.

|br|

Copernicus Marine Environment Monitoring Service
`````````````````````````````````````````````````
The `Copernicus Marine Environment Monitoring Service <https://marine.copernicus.eu/>`_ provides regular and systematic information on the physical and biogeochemical state, variability and dynamics of the ocean and marine ecosystems.

For example, the Copernicus Marine Environment Monitoring Service improves ship routing services, offshore operations or search and rescue operations. The service also contributes to the protection and sustainable management of living marine resources. And the physical and biogeochemical components are useful for water quality monitoring, pollution control, or coastal erosion assessment.

Overall, the service focuses on four main areas:

- Marine safety,
- Marine resources,
- Coastal and marine environment,
- Weather, seasonal forecasting and climate.

.. hint:: **Small activity** |br|
	See past, present and future quality of the marine environment: `My Ocean <https://cmems.lobelia.earth/data?view=viewer&crs=epsg%3A4326&t=1607385600000&z=0&center=-20%2C29&zoom=11&layers=W3siaWQiOiJjMCIsImxheWVySWQiOiJHTE9CQUxfQU5BTFlTSVNfRk9SRUNBU1RfQklPXzAwMV8wMjgvZ2xvYmFsLWFuYWx5c2lzLWZvcmVjYXN0LWJpby0wMDEtMDI4LWRhaWx5L2NobCIsInpJbmRleCI6MCwiaXNIaWRkZW4iOnRydWUsImxvZ1NjYWxlIjp0cnVlfSx7ImlkIjoiYzEiLCJsYXllcklkIjoiR0xPQkFMX0FOQUxZU0lTX0ZPUkVDQVNUX1BIWV8wMDFfMDI0L2dsb2JhbC1hbmFseXNpcy1mb3JlY2FzdC1waHktMDAxLTAyNC90aGV0YW8iLCJ6SW5kZXgiOjEwLCJsb2dTY2FsZSI6ZmFsc2V9XQ%3D%3D&initial=1>`_.

.. seealso:: For additional information, see the `Copernicus Marine Environment Monitoring Service web site <https://marine.copernicus.eu/>`_.

|br|

Copernicus Land Monitoring Service
````````````````````````````````````
The `Copernicus Land Monitoring Service <https://land.copernicus.eu/>`_ provides geographical information on land cover and its changes, land use, vegetation state, water cycle and Earth’s surface energy variables.

For example, the Copernicus Land Monitoring Service supports applications such as spatial and urban planning, forest management, water management, agriculture and food security, nature conservation and restoration, rural development, ecosystem accounting and mitigation/adaptation to climate change.

Overall, the service focuses on five main areas:

- The systematic monitoring of biophysical parameters,
- Land cover and land use mapping,
- Thematic hot-spot mapping,
- Imagery and reference data,
- European ground motion activity.

.. hint:: **Small activity** |br|
	See the `CORINE land cover map of Europe for 2018 <https://land.copernicus.eu/pan-european/corine-land-cover/clc2018>`_.

.. seealso:: For additional information, see the `Copernicus Land Monitoring Service web site <https://land.copernicus.eu/>`_.

|br|

Copernicus Climate Change Service
````````````````````````````````````
The `Copernicus Climate Change Service <https://climate.copernicus.eu/>`_ provides information about the past, present and future climate in Europe and the rest of the World.

For example, The Copernicus Climate Change Service provides scientists, consultants, planners, policymakers, media and the general public free and open access to climate data and tools to assess climate change impacts on biodiversity.

.. hint:: **Small activity** |br|
	See Copernicus `climate data in action <https://climate.copernicus.eu/data-action>`_.

.. seealso:: For additional information, see the `Copernicus Climate Change Service web site <https://climate.copernicus.eu/>`_.

|br|

Copernicus Security Service
````````````````````````````
The `Copernicus Security Service <https://climate.copernicus.eu/>`_ provides information in response to Europe’s security challenges.

For example, the Copernicus Security Service supports the reduction of illegal immigrants’ death at sea, increases the European Union’s internal security, and fights against cross-border crime. It also increases navigation safety, supports fisheries control, combats marine pollution, and law enforcement at sea. Besides, the Copernicus Security Service provides decision-makers with geo-information on remote and difficult to access areas, where security issues are at stake.

Overall, the service focuses on three main areas:

- Border surveillance,
- Maritime surveillance,
- Support to EU external action.

.. hint:: **Small activity** |br|
	See how Copernicus Security can `support evacuation plans <https://sea.security.copernicus.eu/categories/support-to-evacuation-plan/>`_.

.. seealso:: For additional information, see the `Copernicus Security Service web site <https://climate.copernicus.eu/>`_.

|br|

.. _Copernicus-Emergency-Management-Service:

Copernicus Emergency Management Service
````````````````````````````````````````
The `Copernicus Emergency Management Service <https://emergency.copernicus.eu/>`_ provides all actors involved in managing natural disasters, man-made emergency situations, and humanitarian crises with timely and accurate satellite-based geospatial information completed by available on-site data or open data sources.

For example, the Copernicus Emergency Management Service provides digital and printed maps to Civil Protection Authorities and Humanitarian Aid Agencies. Map products can support all the phases of the emergency management cycle: preparedness, prevention, disaster risk reduction, emergency response and recovery.

Overall, the service focuses on two main areas (and four systems):

- The mapping component,
- The early warning component:

- The European Flood Awareness System, which provides overviews on ongoing and forecasted floods in Europe up to 10 days in advance,
- The European Forest Fire Information System, which provides near real-time and historical information on forest fires and forest fire regimes in the European, Middle Eastern and North African regions,
- The European Drought Observatory, which provides drought-relevant information and early-warnings for Europe,
- Global Flood Awareness System, Global Wildfire Information System and Global Drought Observatory complete the previous three systems globally.

.. hint:: **Small activity** |br|
	See the Copernicus Emergency Management system for `flood monitoring and forecast <https://www.efas.eu/efas_frontend/#/home>`_.

.. seealso:: For additional information, see the `Copernicus Emergency Management Service web site <https://emergency.copernicus.eu/>`_.

|br|

(v.11.03.20-10.15)