.. include:: ../html_lat.txt

Principles of image analysis 
=============================

.. _3.2.1:

The spectral signature
-----------------------

.. _What-is-a-spectral-signature:

What is a spectral signature
`````````````````````````````
Each natural and manmade material reflects the sunlight depending on its *chemical composition*, *physical properties*, *texture*, *moisture*, *surface roughness*, and *alteration or degradation state*. |br|
This reflected sunlight is called **reflectance** and is represented with the symbol :math:`\rho`.

In other words, the material’s properties and status define the brightness (i.e. the **reflectance**) of the “colours” (i.e. the **wavelengths**) sensed in the different “lights” (i.e. the **spectral bands**). |br|
This variation of reflectance with wavelengths is called **spectral signature**.

Since each material has a unique spectral signature (like a fingerprint), that means:

- If we know the object material, we can use its spectral signature to monitor health status or degradation (for more details see :ref:`Spectral-indices-for-environmental-monitoring`. For exercises see :ref:`Monitoring-lake-trophic-state` and :ref:`Monitoring-crops-vegetative-stage`),
- If we don’t know the object material, we can use its spectral signature for its identification (for more details see :ref:`Automatic-land-cover-mapping`. For exercises see :ref:`Mapping-crop-types`).

.. note:: **The acquisition of images in the VISIBLE, NEAR INFRARED, and SHORT-WAVE INFRARED spectral bands and the analysis of their spectral signatures is the principles of multispectral Earth observation.**

When studying the Earth’s ecosystems, we are interested in monitoring our planet’s changes. :numref:`Fig1_signature` shows the distribution of the main land covers on Earth.

.. _Fig1_signature:
.. figure:: /img/3/Fig1_signature.png
	:align: center

	Distribution of main land covers on Earth.

Thus, we use satellites to study how such land covers’ spectral signatures change in time. |br|
:numref:`Fig2_signature` - :numref:`Fig7_signature` show the typical spectral signatures of the main land covers.

.. _Fig2_signature:
.. figure:: /img/3/Fig2_signature.png
	:align: center

	Typical spectral signature of clear water (open Ocean).

.. _Fig3_signature:
.. figure:: /img/3/Fig3_signature.png
	:align: center

	Typical spectral signatures of snow and ice.

.. _Fig4_signature:
.. figure:: /img/3/Fig4_signature.png
	:align: center

	Typical spectral signature of clouds.

.. _Fig5_signature:
.. figure:: /img/3/Fig5_signature.png
	:align: center

	Typical spectral signature of bare soil (unvegetated).

.. _Fig6_signature:
.. figure:: /img/3/Fig6_signature.png
	:align: center

	Typical spectral signature of healthy vegetation.

.. _Fig7_signature:
.. figure:: /img/3/Fig7_signature.png
	:align: center

	Typical spectral signatures of clear water (open Ocean) and polluted water (coastal water with chlorophyll content).

.. hint:: **Small activity** |br|
	Try the `Remote Sensing Virtual Lab <https://remotesensinglab.com/measuring.html>`_ to see the spectral signatures of the land covers (cretits: Karen Joyce).

|br|

How to measure spectral signatures with satellites
````````````````````````````````````````````````````
Remember that satellites record the surface reflectance in different spectral bands and produce multiband grayscale images (:ref:`Spectral-characteristics`).

Thus, if we look at a single image pixel and plot its values stored in all the multiband image’s spectral bands, **we approximate its continuous spectral signature with a polyline** *(a line made of segments)*. :numref:`Fig8_signature` shows an example.

.. _Fig8_signature:
.. figure:: /img/3/Fig8_signature.png
	:align: center

	How to calculate the spectral signature with satellite images.

.. warning:: **Remember to use ONLY atmospherically corrected images!** |br|
	Multispectral satellite images capture both the sunlight reflected by the Earth’s surface and the light scattered by the atmosphere. However, when monitoring the environment, **atmospheric scattering is a noise** that must be removed before image manipulation or analysis.

|br|

.. _How-to-compare-spectral-signatures:

How to compare spectral signatures
````````````````````````````````````
Spectral signatures are curves that describe the variation of reflectance with wavelengths :ref:`What-is-a-spectral-signature`. The closer the curves are, the more they are similar. |br|
Unfortunately, it is difficult to calculate the “distance” between curves.

Let’s build a reference system made of orthogonal axes that reproduce reflectances in each spectral band. This reference system is called **feature space** and has **ONE AXIS FOR EACH SPECTRAL BAND**. |br|
In the feature space, the spectral signatures become points (:numref:`Fig8bis_signature`).

.. _Fig8bis_signature:
.. figure:: /img/3/Fig8bis_signature.png
	:align: center

	Top: Multispectral satellite image. Centre: spectral signatures extracted from the satellite image. Bottom: spectral signatures plotted in the feature space.

Now, it is simple to calculate the spectarl signatures' **similarity**: the closer the points are, the more they are similar. |br|
The *Euclidean distance* is often used. Equation :eq:`eqSIG1` shows the formula for two points (1 and 2) in 3-D feature space:

.. math:: \sqrt{\left|x_2-x_1\right|^2+\left|y_2-y_1\right|^2+\left|z_2-z_1\right|^2}
   :label: eqSIG1

where: |br|
1 is the first spectral signature, |br|
2 is the second spectral signature, |br|
x is the axis for spectral band 1, |br|
y is the axis for spectral band 2, |br|
z is the axis for spectral band 3.

.. note:: Usually, satellite images have more than 3 spectral bands. Thus, the feature space has more than 3 axes.

.. note:: About spectral signatures in the feature space:

	- Spectral signatures (curves) are transformed into points, |br|
	- Similar spectral signatures are points close to each, |br|
	- Image pixels with similar spectral signatures are grouped into a **cluster** (called **spectral class**).

|br|
|br|

.. _Spectral-indices-for-environmental-monitoring:

.. _3.2.2:

Spectral indices for environmental monitoring
----------------------------------------------

What is a spectral index
`````````````````````````
A spectral index is a math expression applied to a multispectral image to highlight specific properties of different land covers, their state of alteration, amount or health.

Spectral indices combine the reflectance information from multiple spectral bands into **ONE** numeric value. Thus, they turn satellite images *from a qualitative visual inspection tool into a quantitative numerical analysis tool.* |br|
:numref:`Tab1_SI` shows the most common mathematical formulas.

.. _Tab1_SI:
.. table:: Spectral indices.

   ===================================  =============================================  ===============================================================================  ============================================================
   Family                               Pros                                           Cons                                                                             Example
   ===================================  =============================================  ===============================================================================  ============================================================
   Difference                           Simple                                         Absolute values might depend on external factors (e.g. atmospheric disturbance)  `CRI <https://www.indexdatabase.de/db/i-single.php?id=254>`_
   Ratio                                Less affected by residual atmospheric effects  Unbounded range of values                                                        `RVI <https://www.indexdatabase.de/db/i-single.php?id=72>`_
   Normalized                           Can be used to compared different situations   Are not linear                                                                   `NDVI <https://www.indexdatabase.de/db/i-single.php?id=58>`_
   Any complex mathematical expression  Could map the phenomenon more accurately       Might be challenging to handle or interpret                                      `EVI <https://www.indexdatabase.de/db/i-single.php?id=16>`_
   ===================================  =============================================  ===============================================================================  ============================================================

The most popular spectral indices are those to retrieve the status of vegetation and crops. However, there are also indices designed to:

- Estimate soil properties,
- Delineate burned areas,
- Monitor built-up features,
- Map water bodies,
- Estimate the abundance of minerals or lithotypes,
- Evaluate the snow cover,
- And many others.

|br|

.. _Examples-of-spectral-indices-for-studying-vegetation:

.. _3.2.2.2:

How spectral indices are designed 
````````````````````````````````````
Every land feature reflects the sunlight differently (the spectral signature), depending on their physical state, chemical composition, moisture content, state of alteration (e.g. weathering) or health (for vegetation). Besides, any variation of these parameters produces a corresponding modification in the spectral signature.

Let's see some examples for vegetation.

Look at the spectral signature of a vegetated image pixel (:numref:`Fig1_SI`). |br|
The gap between the low reflectance in the Red band (due to chlorophylls), and the high reflectance in the NIR band (due to internal leaf structure) is an indicator of the greenness of the biosphere.

.. _Fig1_SI:
.. figure:: /img/3/Fig1_SI.png
	:align: center

	Spectral signature of a decidous tree with highlighted the gap between the Red and NIR.

In the example of :numref:`Fig1_SI`, we have  :math:`\rho_{Red}=0.05` and :math:`\rho_{NIR}=0.55`.

Moreover, the more vigour the vegetation is, or the more green biomass is present, the larger this gap is (:numref:`Fig2_SI`). Thus, the difference between NIR and Red reflectances is used as a proxy for overall "amount and health" of green vegetation.

.. _Fig2_SI:
.. figure:: /img/3/Fig2_SI.png
	:align: center

	Colours and spectral signatures of healthy and senescing leaves.

|br|

**Ratio Vegetation Index (RVI)** |br|
This is the basic greenness vegetation index and it is effective over a wide range of different conditions. Equation :eq:`eqSI1` shows its simple mathematical formula:

.. math:: RVI=\frac{\rho_{NIR}}{\rho_{Red}}
   :label: eqSI1

RVI is a positive index (:math:`RVI\geq0`). The larger the ratio, the more “amount of green and healthy vegetation” is present in the image pixel.

In the example of :numref:`Fig1_SI`, we have:

.. math:: RVI=\frac{0.55}{0.05}=11

Typical values for vegetation cover range from **RVI=4** (parse or sick vegetation) up to **RVI=30** (very dense and very healthy vegetation). |br|
Healthy vegetation generally falls between values of 4 to 10.

.. note:: Unfortunately, RVI is not bounded from above. That makes difficult to compare values for different vegetation covers.

|br|

**Normalized Difference Vegetation Index (NDVI)** |br|
This is the most known and used greenness vegetation index. Equation :eq:`eqSI2` shows its mathematical formula:

.. math:: NDVI=\frac{\rho_{NIR}-\rho_{Red}}{\rho_{NIR}+\rho_{Red}}
	:label: eqSI2

NDVI is a normalized index ranging from -1 to 1, but for **VEGETATED LANDS** it has positive values. The larger the ratio, the more “amount of green and healthy vegetation” is present in the image pixel.

In the example of :numref:`Fig1_SI`, we have:

.. math:: NDVI=\frac{0.55-0.05}{0.55+0.05}=0.83

The threshold **NDVI=0.2** is often used to differentiate bare ground (NDVI<0.2) from vegetated land (NDVI>0.2). Thus:

- Moderate values (**0.2<NDVI<0.6**) are typical for shrubs, grass and crops,
- Higher values (**NDVI>0.6**) are typical for forests.

Opposite to RVI, **FOR VEGETATION COVER** NDVI is bounded from below (often NDVI=0.2) and bounded from above (NDVI=1). Thus, it is a useful index to compare different vegetation covers and types.

.. tip:: **Vegetation amount vs health** |br|
	If we are looking at a mixed image pixel with healthy vegetation, then:

	- Moderate values (**0.2<NDVI<0.4**) are typical for sparse vegetation,
	- Intermediate values (**0.4<NDVI<0.6**) are typical for moderately-density vegetation,
	- And higher values (**NDVI>0.6**) are typical for high-density vegetation.

	On the other hand, if we are looking at a fully covered vegetated image pixel:

	- Moderate values (**0<NDVI<0.2**) are typical for very sick vegetation,
	- Intermediate values (**0.2<NDVI<0.6**) are typical for moderately healthy vegetation,
	- And higher values (**NDVI>0.6**) are typical for very healthy vegetation.

While NDVI is meaningful ONLY for vegetated areas, it can be calculated for all land covers. In this case, NDVI will have the following values:

- NDVI **close to -1** is a typical value for clear water,
- **-1<NDVI<0** are typical values for polluted water, and for snow or ice,
- NDVI **close to 0** is a typical value for clouds,
- Slightly positive NDVI (**0<NDVI<0.2**) are typical values for bare soil (i.e. soil without vegetation).

.. hint:: **Small activity** |br|
	Most satellite-based crop monitoring systems use NDVI (or similar spectral indices) to show farmers which parts of their fields have more stressed vegetation. |br|
	See `CropSAT <https://cropsat.com/>`_ for a free online demo to highlight where to increase the fertilization rate (suggestion: try the location "Paderno Ponchielli, CR, Italia").

|br|

**Additional spectral indices** |br|
The list of existing spectral indices is very long, but you could build your own spectral index! All you need is the spectral signature of the standard/unaltered state of the land or object you are monitoring and how the phenomenon you are studying affects its reflectance. |br|

For instance, spectral indices can be used to map floodings occurring more frequently due to climate change.

The **Normalized Difference Water Index (NDWI)** is built on the effects of water/moisture on the soil’s spectral signature: with the increasing of water, the ratio :math:`\frac{\rho_{Green}}{\rho_{NIR}}` decreases. Equation :eq:`eqSI3` shows its mathematical formula:

.. math:: NDWI=\frac{\rho_{Green}-\rho_{NIR}}{\rho_{Green}+\rho_{NIR}}
	:label: eqSI3

NDWI is a normalized index ranging from -1 to 1, but for **WATER** it has positive values. The larger the ratio, the more “amount of water” is present in the image pixel. |br|
The threshold **NDWI=0.3** is often used to differentiate non-flooded areas (NDVI<0.3) from flooded areas (NDWI>0.3).

.. warning:: A DIFFERENT spectral index, also called `Normalized Difference Water Index (NDWI) <https://edo.jrc.ec.europa.eu/documents/factsheets/factsheet_ndwi.pdf>`_, (:math:`NDWI=\frac{\rho_{Green}-\rho_{NIR}}{\rho_{Green}+\rho_{NIR}}`) uses NIR and SWIR spectral bands to detect *water stress in vegetation (e.g. drought)*.

.. caution:: The values and thresholds of the spectral indices described above are intended as general recommendations. |br|
	The analyst’s experience can suggest more appropriate values to the specific case study.


.. hint:: **Looking for a specific spectral index?** |br|
	The `Index DataBase <https://www.indexdatabase.de/>`_ is a collection of spectral indices for different applications and sensors. Here you find a selection of `250 spectral indices designed to fit the images of the Sentinel-2 satellite <https://www.indexdatabase.de/db/is.php?sensor_id=96>`_. |br|
	If you like to import these spectral indices into Sentinel Hub EO Browser, try these `javascript <https://custom-scripts.sentinel-hub.com/custom-scripts/sentinel-2/indexdb/>`_.

|br|
|br|

.. _Automatic-land-cover-mapping:

Automatic land cover mapping
-----------------------------

Land cover maps vs land use maps
`````````````````````````````````
Land cover maps describe the geospatial information on different **physical coverages of the Earth’s surface.** They also capture the land cover changes over time. |br|
Example of land cover classes are:

- Farmlands,
- Glaciers,
- Urban areas,
- Forests,
- Lakes.

*A very efficient method to determine the land cover is analysing satellite images.*

On the other hand, land use maps describe **how people use the land and which activities people do in a specific land cover type.** |br|
Some examples of land use classes are:

- Recreational,
- Residential,
- Commercial,
- Industrial.

Remote sensing systems can provide information on physical coverages. Thus *land use cannot be determined by analysing satellite images.*:numref:`Fig1_Maps` shows the difference between land cover and land use.

.. _Fig1_Maps:
.. figure:: /img/3/Fig1_Maps.png
	:align: center

	Land cover map vs land use map for the city of Toronto, Canada (credit: open data - City of Toronto, ESRI).

|br|

.. _Supervised-image-classification:

Supervised image classification
````````````````````````````````
Automatic mapping of land cover classes is done with supervised image classification.

The basic idea is to train a mathematical model to recognise spectral signatures. This is done using the spectral signatures of the **training samples**, which are image pixels selected in sites with **KNOWN land cover** (called *training sites*).

For each class, pick some training samples on the satellite image and label them with their actual land cover (:numref:`Fig9_signature`). Thus, all the categories have a *reference spectral signature* defined by their training samples (often their mean value) and a *label* (i.e. the land cover class). |br|
**Remember to collect training samples for ALL land cover classes you want to map.** Otherwise, some categories will not be recognised!

.. _Fig9_signature:
.. figure:: /img/3/Fig9_signature.png
	:align: center

	Training sites and training samples.

Now we want the classification algorithm to **predict** each image pixel’s **UNKNOWN land cover** based on their spectral signature’s **similarity** with the **KNOWN training samples** (see :ref:`How-to-compare-spectral-signatures`). |br|
The output is a classification map with all the classes defined by the training samples (:numref:`Fig10_signature`).

**In other words, the classification map is a prediction based on the knowledge of some limited training sites.**

.. _Fig10_signature:
.. figure:: /img/3/Fig10_signature.png
	:align: center

	Prediction of the land cover.

.. note:: **How many training samples?** |br|
	Unfortunately, different classification techniques require a different number of (optimal) training samples! |br|
	**SUGGESTION: a starting point for multispectral images like Sentinel-2 or Landsat could be about 200 image pixels for each class.**

|br|

Classification strategies
````````````````````````````
A massive number of classification strategies are used in remote sensing. They have different requirements, constraints and accuracy. |br|
The subject is so vast that we cannot generalize and is out-of-scope for this training.

**Minimum Distance (to Means)** |br|
A simple and popular method is the **Minimum Distance (to Means)** classifier. This technique:

1. Use the training samples (with KNOWN land cover) to calculate a mean spectral signature for each land cover class,
2. Measures the spectral signature of each image pixels with UNKNOWN land cover,
3. Compares 1. and 2.,
4. Assigns each image pixel to the land cover class with the “closest” *(with minimum EUCLIDEAN distance)* spectral signature.

Thus, the Minimum Distance (to Means) classifier labels the image pixels based their “global” distance with the training samples.

.. note:: See :ref:`Mapping-crop-types` to check how the Minimum Distance (to Means) classifier works.

.. hint:: **Small activity** |br|
	Navigate the `CORINE land cover map of Europe <https://www.arcgis.com/home/webmap/viewer.html?url=https%3A%2F%2Fimage.discomap.eea.europa.eu%2Farcgis%2Frest%2Fservices%2FCorine%2FCLC2018_WM%2FMapServer&source=sd>`_.

**Spectral Angle Mapper** |br|
Another simple yet popular method is the **Spectral Angle Mapper** classifier. This technique:

1. Use the training samples (with KNOWN land cover) to calculate a mean spectral signature for each land cover class. *Training samples might be just ONE spectral signature for each land cover class (called endmembers),*
2. Measures the spectral signature of each image pixels with UNKNOWN land cover,
3. Compares 1. and 2.,
4. Assigns each image pixel to the land cover class with the “closest” spectral signature (with minimum ANGULAR distance).

Thus, the Spectral Angle Mapper classifier labels the image pixels based their "angulal" distance with the training samples.

.. hint:: **Small activity** |br|
	See how the Spectral Angle Mapper classifier works (Credit: `rdrr.io <https://rdrr.io/>`_).

.. raw:: html

	<iframe width="100%" height="500px" src="https://rdrr.io/snippets/embed/?code=%23%23%20Load%20libraries%0Alibrary(RStoolbox)%0Alibrary(raster)%0Alibrary(ggplot2)%0A%0A%23%23%20Load%20test%20image%0Adata(lsat)%20%0A%0A%23%23%20Collect%20training%20samples%20%0A%23%23%20First%20location%20is%20water%2C%20second%20is%20open%20agricultural%20vegetation%0Apts%20%3C-%20data.frame(x%20%3D%20c(624720%2C%20627480)%2C%20y%20%3D%20c(-414690%2C%20-411090))%0Atraining_samples%20%3C-%20extract(lsat%2C%20pts)%0Arownames(training_samples)%20%3C-%20c(%22water%22%2C%20%22vegetation%22)%0A%0A%23%23%20Calculate%20spectral%20angles%0Alsat_sam%20%3C-%20sam(lsat%2C%20training_samples%2C%20angles%20%3D%20TRUE)%0A%0A%23%23%20Plot%20spectral%20angles%20(spectral%20signatures'%20similarity)%0Aplot(lsat_sam)%0A%0A%23%23%20Classify%20based%20on%20minimum%20angle%0Alsat_sam%20%3C-%20sam(lsat%2C%20training_samples%2C%20angles%20%3D%20FALSE)%0A%0A%23%23%20Show%20classification%20map%0AggR(lsat_sam%2C%20forceCat%20%3D%20TRUE%2C%20geom_raster%3DTRUE)%20%2B%20%0A%20%20%20%20%20%20%20%20scale_fill_manual(values%20%3D%20c(%22blue%22%2C%20%22green%22)%2C%20labels%20%3D%20c(%22water%22%2C%20%22vegetation%22))%0A%0A%23%23%20Show%20test%20image%0AggRGB(lsat%2C%20stretch%20%3D%20%22lin%22)" frameborder="0"></iframe>

|br|
|br|

.. _Map-validation:

Map validation
---------------

Precision or accuracy?
````````````````````````
Precision and accuracy are often used as synonyms. **But they are not!**

- **Precision** refers to the degree to which repeated attempts (under unchanged conditions) *are close to each other*, independent of their true value. Thus, a precise quantity might be completely wrong because biased!,
- **Accuracy** refers to the degree to which repeated attempts (under unchanged conditions) *are close to the true value.* **Thus, an accurate attempt is precise and not biased.**

Let’s see how precision and accuracy work. Assume that two archers are participating in a tournament.

The first archer always hit the same spot. He is **precise**. |br|
However, his arrows are systematically displaced from the target’s centre (:numref:`Fig1_validation`). Thus, the second archer is **inaccurate**.

.. _Fig1_validation:
.. figure:: /img/3/Fig1_validation.png
	:scale: 30%
	:align: center

	The first archer's shots.

The second archer fires all his arrows grouped in the target’s centre (:numref:`Fig3_validation`). |br|
The archer is precise and unbiased. Thus, the first archer is **accurate**.

.. _Fig3_validation:
.. figure:: /img/3/Fig3_validation.png
	:scale: 30%
	:align: center

	The second archer's shots.

.. hint:: For a land cover map:

	- **Accuracy** refers to the degree to which *the information on the map* matches the real world, |br|
	- **Precision** refers to how exactly is *the data used to create the map*. This is also related to its spatial resolution, spectral characteristics, or time of acquisition (see :ref:`Fundamentals-of-remote-sensing-and-Earth-observation`).

|br|

How much is accurate a map?
````````````````````````````
Referring to the mapping process, **accuracy** is the most used performance metric and tells *“how many sites are mapped correctly.”*

Map accuracy is estimated using the **confusion matrix**, a table that relates the actual land cover of some KNOWN reference locations, called the *testing samples*, with their predicted values in the map. |br|

:numref:`Fig1_confmatrix` shows an example of a confusion matrix computed for a 4-class thematic map. In this table:

- Columns represent the instances of testing samples in the actual land cover class,
- Rows represent the instances of testing samples in the predicted land cover class,
- Instances belonging to the main diagonal (green cells) are the number of testing samples classified correctly.

.. _Fig1_confmatrix:
.. figure:: /img/3/Fig1_confmatrix.png
	:align: center

	Confusion matrix. Number of testing samples correctly classified.

:numref:`Fig2_confmatrix` highlights the number of misclassified testing samples (red cells). |br|
Overall, the confusion matrix has **434 testing samples.**

.. _Fig2_confmatrix:
.. figure:: /img/3/Fig2_confmatrix.png
	:align: center

	Confusion matrix. Number of misclassified testing samples.

.. note:: **What are the testing samples?** |br|
	To evaluate the map’s accuracy, we must compare predicted land cover classes with actual land cover classes. This is done using the testing samples, which are image pixels randomly collected, but those actual land cover is KNOWN. Results are then extended from the testing samples to the full map.

	**GUIDELINE: testing samples must be randomly collected for ALL land cover classes. There should be no less than 50 testing samples for each land cover class.**

**a. Overall accuracy** |br|
Suppose we want to quantify the proportion of correct predictions, without giving any insight into the single accuracy of land cover classes. *In other words, how many testing samples are globally labelled correctly in the classified map?* |br|
It is called **overall accuracy** and is usually expressed as a percent, with 0% being a perfect misclassification and 100% being a perfect classification:

.. math:: Overall\ accuracy=\frac{sum\ of\ testing\ samples\ being\ correctly\ classified}{total\ number\ of\ testing\ sample}
	:label: eqacc1

In the example of :numref:`Fig1_confmatrix` we have:

.. math:: Overall\ accuracy=\frac{65+81+85+90}{434}=74.0 \%
	:label: eqacc2

.. note:: The overall accuracy is the primary indicator used to evaluate maps.

|br|

**b. Producer’s accuracy** |br|
Suppose we want to quantify the proportion of correct predictions for each of the real-world land cover class. *In other words, for a given land cover class in the real world, how many testing samples are labelled correctly in the classified map?* |br|
This is the accuracy from the point of view of the mapmaker (the producer). It is called **producer’s accuracy** and is usually expressed as a percent, with 0% being a perfect misclassification and 100% being a perfect classification:

.. math:: Producer\prime s\ accuracy\ for\ class\ i=\frac{number\ of\ testing\ samples\ being\ correctly\ classified\ in\ class\ i}{total\ number\ of\ testing\ sample\ in\ column\ i}
	:label: eqacc3

In the example of :numref:`Fig1_confmatrix` we have:

.. math:: Producer\prime s\ accuracy\ for\ class\ A=\frac{65}{65+6+0+4}=86.7 \%
	:label: eqacc4

.. math:: Producer\prime s\ accuracy\ for\ class\ B=\frac{81}{4+81+11+7}=78.6 \%
	:label: eqacc5

.. math:: Producer\prime s\ accuracy\ for\ class\ C=\frac{85}{22+5+85+3}=73.9 \%
	:label: eqacc6

.. math:: Producer\prime s\ accuracy\ for\ class\ D=\frac{90}{24+8+19+90}=63.8 \%
	:label: eqacc7

Thus, the classifier is mapping real world class A with higher accuracy.

.. note:: The producer's accuracy is an indicator of how well the actual land cover information is mapped.

|br|

**c. User’s accuracy** |br|
Suppose we want to quantify the proportion of correct predictions for each of the mapped classes. *In other words, for a given class in the map, how many testing samples are really present on the ground?* |br|
This is the accuracy from the point of view of the map user. It called is called **user’s accuracy** and is usually expressed as a percent, with 0% being a perfect misclassification and 100% being a perfect classification:

.. math:: User\prime s\ accuracy\ for\ class\ i=\frac{number\ of\ testing\ samples\ being\ correctly\ classified\ in\ class\ i}{total\ number\ of\ testing\ sample\ in\ row\ i}
	:label: eqacc8

In the example of :numref:`Fig1_confmatrix` we have:

.. math:: User\prime s\ accuracy\ for\ class\ A=\frac{65}{65+4+22+24}=56.5 \%
	:label: eqacc9

.. math:: User\prime s\ accuracy\ for\ class\ B=\frac{81}{6+81+5+8}=81.0 \%
	:label: eqacc10

.. math:: User\prime s\ accuracy\ for\ class\ C=\frac{85}{0+11+85+19}=73.9 \%
	:label: eqacc11

.. math:: User\prime s\ accuracy\ for\ class\ D=\frac{90}{4+7+3+90}=86.5 \%
	:label: eqacc12

Thus, the classifier is predicting the map’s class A with lower accuracy.

Typically, user’s and producer’s accuracy for a given land cover class are different. In the example of :numref:`Fig1_confmatrix`, 86.7% of the testing samples for real-world class A are correctly identified as class A in the map (producer’s accuracy). However, only 56.5% of the areas identified as class A in the map are actually being class A on the ground.

.. note:: The user's accuracy is an indicator of how well the map describes the actual land covers.

.. hint:: **Small activity** |br|
	Which is the accuracy of your map? |br|
	Calculate the overall accuracy and the per-class producer’s accuracy and user’s accuracy of your own map. Try the free `Confusion matrix online calculator <http://www.marcovanetti.com/pages/cfmatrix/>`_.

.. seealso:: For additional information, see the practical guide on `Map Accuracy Assessment and Area Estimation <http://www.fao.org/3/i5601e/i5601e.pdf>`_ of `FAO <http://www.fao.org/home/en/>`_.

|br|

(v.11.03.20-10.15)