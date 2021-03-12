.. include:: ../html_lat.txt

.. _3.4:

Hands-on exercises
===================

.. _Monitoring-lake-trophic-state:

Monitoring lake’s trophic state (difficulty: advanced)
-------------------------------------------------------

Download the data
````````````````````
.. important:: **DATA FOR THE EXERCISE** |br|
   `Click here to download the data for this exercise (1.1 GB). <https://drive.google.com/file/d/1p4a8IUE0RGNIK4ARXXOYMti_IgG-SIJn/view?usp=sharing>`_

|br|

The environmental problem
````````````````````````````
The trophic state of a water body describes the amount of nutrients (mainly phosphorus and nitrogen) available to grow aquatic vegetation and phytoplankton. However, when water becomes rich with nutrients, phytoplankton’s rapid growth (called **algae bloom**) could cause negative impacts on the marine environment, like:

- The disruption of the normal ecosystem functioning,
- The consumption of oxygen in the water, resulting in the death of aquatic organisms and fishes,
- The reduction of sunlight reaching aquatic plants under the water surface,
- The production of harmful toxins.

Lakes are usually classified into 4 trophic states, according to chlorophyll’s concentration present in the water. :numref:`Tab1_WQ` shows the most common definitions.

.. _Tab1_WQ:
.. table:: Chlorophyll’s concentration and trophic level of lakes.

   ==============  ===========================  ====================================
   Trophic level   Chlorophyll’s concentration  Primary productivity
   ==============  ===========================  ====================================
   Oligotrophic    0-2.6 mg/m3                  Low due to nutrient deficiency
   Mesotrophic     2.6-20 mg/m3                 Intermediate
   Eutrophic       20-56 mg/m3                  High due to excessive nutrients
   Hypereutrophic  >56 mg/m3                    Very High due to excessive nutrients
   ==============  ===========================  ====================================

.. Warning:: **The role of climate change** |br|
   Climate change may indirectly cause eutrophication by increasing runoff from the land, affecting nutrient load, due to increased precipitation resulting from global warming.

|br|

Scope of the exercise
````````````````````````
This exercise shows a very simple method to monitor the eutrophic level of a lake with satellites.

|br|

.. _Study-area:

Study area
````````````
Lake Trasimeno is located in central Italy, in the Umbria region on the border with Tuscany. The lake is the fourth for surface area in Italy (mean surface area 121 km2), has two minor tributaries but none natural emissaries, and is surrounded by a natural park. |br|
The lake is very shallow (4-5 m average depth). Its water level is usually at the highest level in April/May (less than 6 m) and at the minimum level in September/October. For its peculiar characteristics, in summer Lake Trasimeno is prone to eutrophication.

|br|

Satellite images
`````````````````
The analysis is done using ten cloud-free Sentinel-2 images collected in the following dates of Summer 2016:

- 18 July 2016,
- 4 August 2016,
- 14 August 2016,
- 24 August 2016,
- 27 August 2016,
- 3 September 2016,
- 13 September 2016,
- 23 September 2016,
- 26 September 2016.

.. warning:: **Remember to use ONLY atmospherically corrected images!** |br|
   Today (February 2021), Sentinel-2 data collected on 2016 are only provided as ``L1C`` products. That means these satellite images are NOT corrected for the atmospheric disturbance. Thus, **they are NOT ready for image processing!**

   Atmospheric correction is an advanced topic not covered in training. Thus, this exercise uses the most simple atmospheric compensation technique, called Dark Object Subtraction (DOS), to derive pseudo ``L2A`` products.

|br|

.. _The-modelling-WQ:

The modelling
````````````````
The Ratio Vegetation Index (RVI) is a spectral index proportional to chlorophyll’s concentration. Thus, it could be used as a proxy for its estimation. |br|
Phytoplankton are microorganisms that float on the water body and contain chlorophyll. Thus, they could be detected with RVI.

In this exercise we use a simple linear regression model described by equation :eq:`eqWQ1`:

.. math:: Chl\ \left[mg/m^3\right]=a\times RVI+b
   :label: eqWQ1

For Sentinel-2 images, we calculate Equation :eq:`eqWQ1` as follows:

.. math:: Chl\ \left[mg/m^3\right]=a\times\frac{\rho_{Band 4}}{\rho_{Band 3}}+b
   :label: eqWQ2

|br|

Chlorophyll’s concentration and water level
````````````````````````````````````````````
The Ratio Vegetation Index (RVI) is proportional to chlorophyll’s concentration, but it does not represent its exact value. Thus, we need some experimental data of known chlorophyll’s concentration vs RVI value for the calibration of the equation :eq:`eqWQ2`.

:numref:`Fig1_WQ` shows Lake Trasimeno with superimposed five sampling locations (green dots) where the chlorophyll’s concentration was measured on 18 July 2016. These data are used for the model’s calibration.

.. _Fig1_WQ:
.. figure:: /img/3/Fig1_WQ.png

   Lake Trasimeno with superimposed the sampling locations (green dots).

.. _Tab2_WQ:
.. table:: Lake Trasimeno: chlorophyll concentration sampled on 18 July 2016.

   ======  ===============================================  ===================
   Site #  Coordinates E, N (WGS84 - UTM 32N (EPSG:32632))  Chlorophyll [mg/m3]
   ======  ===============================================  ===================
   1       754795, 4783085                                  20.5
   2       751675, 4778175                                  12.5
   3       753995, 4781525                                  19.0
   4       755425, 4776475                                  15.0
   5       747955, 4784225                                  18.0
   ======  ===============================================  ===================

.. _Tab3_WQ:
.. table:: Lake Trasimeno: water level changes in summer 2016.

   =========  ====================================================
   Month      Water level changes (compared to the previous month)
   =========  ====================================================
   May        +2 m
   June       -2 m
   July       -12 m
   August     -16 m
   September  -5 m
   October    +2 m
   =========  ====================================================

|br|

.. _3.4.1.8:

QGIS set-up
`````````````
Open QGIS. Go to the menu bar and click ``Plugins`` → ``Manage and Install Plugins...`` (:numref:`Fig3_WQ_Plugins`).

.. _Fig3_WQ_Plugins:
.. figure:: /img/3/Fig3_WQ_Plugins.png

   Sample screenshot.

In the search bar write **SCP** and select the ``Semi-Automatic Classification Plugin``. Press ``Install plugin`` in the bottom-right corner of the window and close the window (:numref:`Fig4_WQ_Install_Plugin`).

.. _Fig4_WQ_Install_Plugin:
.. figure:: /img/3/Fig4_WQ_Install_Plugin.png

   Sample screenshot.

In QGIS main window, select ``New Empty Project`` (:numref:`Fig2_WQ_New_Project`).

.. _Fig2_WQ_New_Project:
.. figure:: /img/3/Fig2_WQ_New_Project.png

   Sample screenshot.

|br|

Prepare the satellite images
````````````````````````````````
Open the Semi-Automatic Classification Plugin (SCP) (:numref:`Fig5_WQ_Open_SCP`).

.. _Fig5_WQ_Open_SCP:
.. figure:: /img/3/Fig5_WQ_Open_SCP.png

   Sample screenshot.

In the left-side window open ``Preprocessing`` → ``Sentinel-2`` (:numref:`Fig6_WQ_Import_Sentinel2`). This tool provides the pre-processing tasks to prepare the satellite images for the analysis.

.. _Fig6_WQ_Import_Sentinel2:
.. figure:: /img/3/Fig6_WQ_Import_Sentinel2.png

   Sample screenshot.

Select the following parameters (:numref:`Fig7_WQ_Import_Sentinel2_part2`):

- ``Directory containing Sentinel-2 bands:`` open the folder ``..\GIS_4_School\4.1_Monitoring_lake_trophic_state`` → ``S2A_MSIL1C_20160718T101032_N0204_R022_T32TQN_20160718T101028.SAFE`` → ``S2A_MSIL1C_20160718T101032_N0204_R022_T32TQN_20160718T101028.SAFE`` → ``GRANULE`` → ``L1C_T32TQN_A005596_20160718T101028`` → ``IMG_DATA``,
- ``Select metadata file (MTD_MSI):`` select the file **MTD_MSIL1C** in the folder ``S2A_MSIL1C_20160718T101032_N0204_R022_T32TQN_20160718T101028.SAFE`` → ``MTD_MSIL1C``,
- ``Apply DOS1 atmospheric correction:`` select this option. This command applies the simple DOS atmospheric correction to the satellite images.

Click the button **RUN** and select the output directory (:numref:`Fig7_WQ_Import_Sentinel2_part2`).

.. _Fig7_WQ_Import_Sentinel2_part2:
.. figure:: /img/3/Fig7_WQ_Import_Sentinel2_part2.png

   Sample screenshot.

The outcomes of this processing are 10 spectral bands:

- 4 bands with 10-meters spatial resolution saved in GeoTiff format,
- 6 bands (with original 20-meters spatial resolution) resampled to match the 10-meters spatial resolution of the first 4 bands, saved in GeoTiff format.

Now we want to merge all the spectral bands in a single image. This is called **multiband image** (or **multispectral image**).

In the Semi-Automatic Classification Plugin window, select **Band set** (Upper left corner) and flag the option **Create raster of band set (stack bands)** (:numref:`Fig8_CROP_20m_wrong_band_order`).

Click the button **RUN** and select the output directory (:numref:`Fig8_WQ_Create_Stack`). The output file will be named as the input bands followed by ``stack_raster``.

.. _Fig8_WQ_Create_Stack:
.. figure:: /img/3/Fig8_WQ_Create_Stack.png

   Sample screenshot.

Remove from QGIS all the layer, except ``RT_T32TQN_20160718T101032_B0stack_raster``. To remove a layer, right-click the layer in the windows **Layers** and select ``Remove layer``.

The image is loaded in QGIS. However, its colours are not what we expect because the satellite’s spectral bands are not loaded in the correct order (:numref:`Fig9_WQ_Sentinel2_Visaulization`).

.. _Fig9_WQ_Sentinel2_Visaulization:
.. figure:: /img/3/Fig9_WQ_Sentinel2_Visaulization.png

   Sample screenshot.

To solve this problem, we need to tell QGIS which spectral bands correspond to Red, Green and Blue.

|br|

.. _Load-the-satellite-images-with-the-correct-colours:

Load the satellite images with the correct colours
````````````````````````````````````````````````````
Right-click on the image name → ``Properties`` → ``Symbology`` and set (:numref:`Fig10_WQ_Layer_Symbology`):

- ``Red band:`` set ``Band 03``. The satellite’s band 3 collects the Red reflected sunlight,
- ``Green band:`` set ``Band 02``. The satellite’s band 2 collects the Green reflected sunlight,
- ``Blue band:`` as ``Band 01``. The satellite’s band 1 collects the Blue reflected sunlight.

Click the button ``Apply`` and then click the button ``OK``.

.. _Fig10_WQ_Layer_Symbology:
.. figure:: /img/3/Fig10_WQ_Layer_Symbology.png

   Sample screenshot.

Now QGIS shows the satellite image with the correct colours (:numref:`Fig11_WQ_True_Color`).

.. _Fig11_WQ_True_Color:
.. figure:: /img/3/Fig11_WQ_True_Color.png

   Sample screenshot.

|br|

Resize the image
````````````````````
The Sentinel-2 images cover a larger area than our study area. Thus, we can resize them before starting the data processing.

Import in QGIS the vector layer ``..\Study_area\trasimeno_proj.shp``.
To resize (i.e. clip) the satellite image, search in the **Processing Toolbox** panel the command **clip** and open the tool **Clip raster by mask layer** in the *GDAL package* (:numref:`Fig13_WQ_Toolbox_Clip`).

.. _Fig13_WQ_Toolbox_Clip:
.. figure:: /img/3/Fig13_WQ_Toolbox_Clip.png

   Sample screenshot.

.. hint:: If the Processing Toolbox panel is not loaded, open the QGIS menu ``View`` → ``Panels`` and select ``Processing Toolbox``.

A new window appears (:numref:`Fig14_WQ_Clip_parameters`). In the **Clip Raster by Mask Layer** window, set the following parameters:

- ``Input layer:`` set ``RT_T32TQN_20160718T101032_B0stack_raster``,
- ``Mask layer:`` set ``Trasimeno_proj``,
- ``Source CRS:`` Not set,
- ``Target CRS:`` Not set,
- ``Assign a specified nodata value to output bands:`` Not set,
- ``Create an output alpha band:`` unselect,
- ``Match the extent of the clipped raster to the extent o the mask layer:`` select,
- ``Keep resolution of input raster:`` select,
- ``Set output file resolution``: unselect,
- ``X Resolution of output bands``: Not set,
- ``Y Resolution of output bands``: Not set,
- ``Clipped (mask):`` Click on the three dots [...]. Select ``Save to file`` and browse to the folder where you saved the merged images. Now save the new resized (clipped) image with the file name ``RT_T32TQN_20160718T101032_Clip``.

.. _Fig14_WQ_Clip_parameters:
.. figure:: /img/3/Fig14_WQ_Clip_parameters.png

   Sample screenshot.

Click the button ``RUN``, then ``CLOSE``.

The new clipped image will appear in QGIS (:numref:`Fig15_WQ_Lake_Clip`). Now the image is smaller; thus, the subsequent data processing will be faster.

.. _Fig15_WQ_Lake_Clip:
.. figure:: /img/3/Fig15_WQ_Lake_Clip.png

   Sample screenshot.

Like it happened when importing the full-size Sentinel-2 image, the resized image is loaded with the wrong order’s spectral bands. Thus, Lake Trasimeno has the wrong colour.

Repeat the steps described in :ref:`Load-the-satellite-images-with-the-correct-colours` (:numref:`Fig16_WQ_Lake_Clip_Symbology`).

.. _Fig16_WQ_Lake_Clip_Symbology:
.. figure:: /img/3/Fig16_WQ_Lake_Clip_Symbology.png

   Sample screenshot.

Now QGIS shows the satellite image with the correct colours (:numref:`Fig17_WQ_Lake_True_color_visualization`).

.. _Fig17_WQ_Lake_True_color_visualization:
.. figure:: /img/3/Fig17_WQ_Lake_True_color_visualization.png

   Sample screenshot.

|br|

Calculate the Ratio Vegetation Index
`````````````````````````````````````
Remember we use the spectral model described in (:ref:`The-modelling-WQ`). Thus we calculate the Ratio Vegetation Index (RVI) (:ref:`Examples-of-spectral-indices-for-studying-vegetation`) with Sentinel-2’s band 3 (B3) and band 4 (B4).

Now we do some calculations with images using the **Raster Calculator**. This tool allows evaluating equations based on the image pixel values. |br|
Open **Raster Calculator** from the menu ``Raster`` → ``Raster Calculator...`` (:numref:`Fig18_WQ_Raster_Calculator`).

.. _Fig18_WQ_Raster_Calculator:
.. figure:: /img/3/Fig18_WQ_Raster_Calculator.png

   Sample screenshot.

Now, we have to write Equation :eq:`eqWQ3` using QGIS syntax, so the software can understand it.

.. math:: RVI=\frac{\rho_{Band 4}}{\rho_{Band 3}}
   :label: eqWQ3

With the help of the calculator buttons, write the following expression in ``Raster Calculator Expression``:

"RT_T32TQN_20160718T101032_Clip@4/RT_T32TQN_20160718T101032_Clip@3"

.. hint:: **How to read QGIS equations?**

   "RT_T32TQN_20160718T101032_Clip@4" means: |br|
   *“pick each pixel value of the resized image RT_T32TQN_20160718T101032_Clip for band 4 (@4)”*.

   "RT_T32TQN_20160718T101032_Clip@3" means: |br|
   *“pick each pixel value of the resized image RT_T32TQN_20160718T101032_Clip for band 3 (@3)”*.

   **Equations are calculated on a pixel basis. Thus the same equation is computed for each image pixel individually. The results are shown in a new image.**

In **Result Layer** click on the three dots ``[...]`` next to ``Output layer`` and select where you want to save the results. Name the file ``Ratio_b4_b3.tif`` (:numref:`Fig19_WQ_Raster_Calculator_expression`).

.. _Fig19_WQ_Raster_Calculator_expression:
.. figure:: /img/3/Fig19_WQ_Raster_Calculator_expression.png

   Sample screenshot.

The output is a grayscale image, where each pixel contains its RVI value just computed (:numref:`Fig20_WQ_B4_b3_Index`).

.. _Fig20_WQ_B4_b3_Index:
.. figure:: /img/3/Fig20_WQ_B4_b3_Index.png

   Sample screenshot.

|br|

Sample the RVI in the calibration sites
````````````````````````````````````````
We know chlorophyll’s concentration in the five calibration sites because it was measured *on site*. But also we need the satellite-derived RVI.

Import in QGIS the layer ``..Points/Sampling_2016.shp``. This file contains five small red polygons where the chlorophyll was sampled (:numref:`Fig21_WQ_Points`).

.. _Fig21_WQ_Points:
.. figure:: /img/3/Fig21_WQ_Points.png

   Sample screenshot.

To extract from the satellite image the RVI of the calibration sites, we use the **Zonal statistics** tool. |br|
Unlike the **Cell Statistics** algorithm that computes per-pixel statistics, the **Zonal statistics** algorithm calculates per-polygon statistics. That means the output (e.g. minimum, maximum, sum, count, *etc.*) is calculated only on pixels within the selected polygons.

Search in the **Processing Toolbox** panel for the **Zonal statistics** (or write *zonal statistics* in the Processing Toolbox search bar) and double-click on it (:numref:`Fig22_WQ_Toolbox_Zonal_Statistics`).

.. _Fig22_WQ_Toolbox_Zonal_Statistics:
.. figure:: /img/3/Fig22_WQ_Toolbox_Zonal_Statistics.png

   Sample screenshot.

.. hint:: If the Processing Toolbox panel is not loaded, open the QGIS menu ``View`` → ``Panels`` and select ``Processing Toolbox``.

The Zonal Statistics window opens. Select the following parameters (:numref:`Fig23_WQ_Zonal_Statistics_parameters`): 

- **Raster layer:** set to ``Ratio_b4_b3``,
- **Raster band:** set to ``Band 1 (Gray)``,
- **Vector layer containing zones:** set to ``Sampling_2016``,
- **Output column prefix:** set to ``b4/b3_``,
- **Statistics to calculate:**

   - Click on the three dots ``[...]``,
   - Select **Mean** and unselect all the other statistics,
   - Click the blue back arrow, located in the upper-left corner.

- **Zonal statistics:**

   - Click on the three dots ``[...]``,
   - Save to file,
   - Select the folder where to save the Zonal Statistics file,
   - Name the file ``b4_b3_mean``.

Click the button ``RUN`` to execute the data processing.

.. _Fig23_WQ_Zonal_Statistics_parameters:
.. figure:: /img/3/Fig23_WQ_Zonal_Statistics_parameters.png

   Sample screenshot.

The data processing adds a new shapefile layer called “b4_b3_mean”. This is the copy of the shapefile “Sampling_2016”, with the addition of the new attribute (i.e. column) **b4/b3_mean**. |br|
This attribute contains the RVI mean value of each polygon (i.e. rows) (:numref:`Fig24_WQ_Points_attribute_table`).

.. _Fig24_WQ_Points_attribute_table:
.. figure:: /img/3/Fig24_WQ_Points_attribute_table.png

   Sample screenshot.

|br|

Calibrate the spectral model
`````````````````````````````
To transform the spectral information of satellites into chlorophyll concentrations, we use the simple linear model of Equation :eq:`eqWQ4`:

.. math:: Chl\ \left[mg/m^3\right]=a\times\frac{\rho_{Band 4}}{\rho_{Band 3}}+b
   :label: eqWQ4

Where *a* and *b* are coefficients (i.e. numbers) we have to compute using the on-site chlorophyll measures. This task is called **model calibration.**

We only have data for 5 calibration sites (very few). Thus we use the strategy:

- Build 5 different calibration sets of chlorophyll measures, using only 4 out of the 5 measures available,
- For each calibration set:

   - Calculate the coefficients *a* and *b* in Equation :eq:`eqWQ4`,
   - Predict the chlorophyll concentration for the fifth calibration site using Equation :eq:`eqWQ4` and the previously computed coefficients *a* and *b*,
   - Compare the estimated concentration with the on-site measure (i.e. the fifth measure left out).

- Select the coefficients *a* and *b* which give the best result.

For this task, we use a pre-compiled spreadsheet (:numref:`Fig25_WQ_Excel`). Open the file ``Regression.xls``,

.. _Fig25_WQ_Excel:
.. figure:: /img/3/Fig25_WQ_Excel.png

   Sample screenshot.

In cells **B2-B6** copy the RVI values for the 5 calibration sites (four decimal digit are enough) (:numref:`Fig26_WQ_Excel_2`).

In cells **C2-C6** copy the on-site measures of chlorophyll concentration (:numref:`Fig26_WQ_Excel_2`).

The spreadsheet automatically calculates the following data:

- Cells **E2** and **F2** show the estimated values for *a* and *b* using only the first 4 points,
- Cells **H2-H6** show the estimated values of chlorophyll concentration for the fifth point that was left out,
- Cells **I2-I6** show the difference between the estimated (column H) and the on-site measured (column C) chlorophyll concentration.

.. note:: The lower cell **I6**, the better the model. This cell shows the difference to the fifth data that was not used for the model calibration. Thus, it describes the accuracy of our model.

.. _Fig26_WQ_Excel_2:
.. figure:: /img/3/Fig26_WQ_Excel_2.png

   Sample screenshot.

Now copy the values of cells **B2-C6** in the other four boxes, but changing their order according to column **A**. This way, the fifth data used for testing the model accuracy is always different (:numref:`Fig27_WQ_Excel_3`).

.. _Fig27_WQ_Excel_3:
.. figure:: /img/3/Fig27_WQ_Excel_3.png

   Sample screenshot.

We see that out of the five repetitions, the second one is the best because it has the lowest difference between estimated and measured chlorophyll concentration (:numref:`Fig27_WQ_Excel_3`).

Consequently, the calibrated model becames Equation :eq:`eqWQ5`:

.. math:: Chl\ \left[mg/m^3\right]=97.95\times\frac{\rho_{Band 4}}{\rho_{Band 3}}-76.09
   :label: eqWQ5

|br|

Create an automatic workflow
`````````````````````````````
Remove all the layers from QGIS and import all the Sentinel-2 images from the folder ``..\GIS_4_School\4.1_Monitoring_lake_trophic_state\Pre-processed``. These images are already corrected for the atmospheric disturbance with the DOS algorithm and are, thus, ready for the processing.

Now we need to repeat the same data processing for ALL the 10 satellite images. This task is very time consuming and also prone to errors. Thus, we automate data processing.

.. important:: QGIS can be programmed with *Python scripts*. However, for most common tasks QGIS can be programmed using a Graphical Modeler that **does not require any programming knowledge.** |br|

Open the Graphical Modeler tool: ``Processing`` → ``Graphical Modeler`` (:numref:`Fig28_WQ_Processing`).

.. _Fig28_WQ_Processing:
.. figure:: /img/3/Fig28_WQ_Processing.png

   Sample screenshot.

The Model Designer window opens (:numref:`Fig29_WQ_Graphical_modeler`). This tool links together single processing steps into a processing workflow.

.. _Fig29_WQ_Graphical_modeler:
.. figure:: /img/3/Fig29_WQ_Graphical_modeler.png

   Sample screenshot.

First, we need to tell the Graphical Modeler that our **Inputs** are Sentinel-2 images. Search for ``Raster Layer`` in the left-side panel and double click it (:numref:`Fig30_WQ_Input_Raster_Layer`).

.. _Fig30_WQ_Input_Raster_Layer:
.. figure:: /img/3/Fig30_WQ_Input_Raster_Layer.png

   Sample screenshot.

The **Raster Layer Parameter Definition** window opens. Type ``Sentinel-2`` in the Description textbox (:numref:`Fig31_WQ_Raster_Layer_Definition`) and click the button ``OK``.

.. _Fig31_WQ_Raster_Layer_Definition:
.. figure:: /img/3/Fig31_WQ_Raster_Layer_Definition.png

   Sample screenshot.

The first “block” of our processing chain is created (:numref:`Fig32_WQ_First_Block`).

.. _Fig32_WQ_First_Block:
.. figure:: /img/3/Fig32_WQ_First_Block.png

   Sample screenshot.

Now we need to build the processing “blocks” to automate:

1. The estimation of chlorophyll concentration,
2. The resizing of data to the study area,
3. The processing of all the satellite images.

In the left-side panel click on the tab ``Algorithms``. The list of available command changes. Search for ``Raster Calculator`` and select the tool ``Raster Calculator`` from the **Raster analysis package** (:numref:`Fig33_WQ_Algorithms_Raster_Calculator`).

.. _Fig33_WQ_Algorithms_Raster_Calculator:
.. figure:: /img/3/Fig33_WQ_Algorithms_Raster_Calculator.png

   Sample screenshot.

The **Raster calculator** window opens (:numref:`Fig34_WQ_Model_Raster_Calculator_Expression`). With the help of the calculator buttons, write the following expression:

97.95*(“Sentinel-2@4”/”Sentinel-2@3”) - 76.09

And set the following parameters (:numref:`Fig34_WQ_Model_Raster_Calculator_Expression`):

- ``Reference layer(s):`` click on the button ``[123]`` and select **Model input** ``Sentinel-2```,
- ``Cell size:`` keep the default value,
- ``Output extent:`` keep the default value,
- ``Output CRS:`` keep the default value,
- ``Output:`` click on the drop-down list and select ``Value``. Type ``_Chl.tif`` and click the button ``OK``.

.. _Fig34_WQ_Model_Raster_Calculator_Expression:
.. figure:: /img/3/Fig34_WQ_Model_Raster_Calculator_Expression.png

   Sample screenshot.

The second “block” appears in the Model Designer window (:numref:`Fig35_WQ_Second_Block`).

.. _Fig35_WQ_Second_Block:
.. figure:: /img/3/Fig35_WQ_Second_Block.png

   Sample screenshot.

We now want to resize (clip) the output of our data processing to match the study area of Lake Trasimano.

Search again in the tab ``Algorithms`` for the command ``Clip``. Click on ``Clip raster by mask layer`` from the **GDAL package**  (:numref:`Fig36_WQ_Algorithms_Clip`).

.. _Fig36_WQ_Algorithms_Clip:
.. figure:: /img/3/Fig36_WQ_Algorithms_Clip.png

   Sample screenshot.

The **Clip raster by mask layer** window opens. Set the following parameters (:numref:`Fig37_WQ_Model_Clip_parameters`):

- ``Input layer:`` click on the button ``[123]`` and select ``Algorithm Output``, and ``“Output” form algorithm “Raster calculator”``,
- ``Mask layer: `` click the dots ``[…]`` and select the file ``../Study_area/trasimeno_proj.shp``,
- ``Source CRS:`` leave it empty,
- ``Target CRS:`` leave it empty,
- ``Assign a specified nodata value to output bands:`` not set,
- ``Create an output alpha band:`` set **no**,
- ``Match the extent of the clipped raster to the extent of the mask layer:`` set **yes**,
- ``Keep resolution of input raster:`` set **yes**,
- ``Set output file resolution:`` set **no**,
- ``X Resolution to output bands:`` not set,
- ``Clipped:`` click on the drop-down list and select ``Model Output``. Type ``_clip.tif`` and click the button ``OK``.

.. _Fig37_WQ_Model_Clip_parameters:
.. figure:: /img/3/Fig37_WQ_Model_Clip_parameters.png

   Sample screenshot.

The last “block” appears in the Model Designer window (:numref:`Fig38_WQ_Third_Block`).

.. _Fig38_WQ_Third_Block:
.. figure:: /img/3/Fig38_WQ_Third_Block.png

   Sample screenshot.

Let’s call our workflow *Chl_Concentration*. In the Model Designer window, type ``Chl_Concentration`` in **Model Properties** (:numref:`Fig39_WQ_Model_Name`).

.. _Fig39_WQ_Model_Name:
.. figure:: /img/3/Fig39_WQ_Model_Name.png

   Sample screenshot.

Finally, save the model: ``Model`` → ``Save model as``, select a folder and save as ``Chl_Concentration`` (:numref:`Fig40_WQ_Save_Model`).

.. _Fig40_WQ_Save_Model:
.. figure:: /img/3/Fig40_WQ_Save_Model.png

   Sample screenshot.

We have created the processing workflow (like if we have written a script) and are ready to launch it.

.. note:: Internally, QGIS transforms the graphical model into a Python code.

|br|

Create a batch processing to manipulate all the satellite images at once
````````````````````````````````````````````````````````````````````````````
We want to monitor the eutrophic level of Lake Trasimeno with Sentinel-2 images. Thus we have to run the processing workflow several times, each one with a different satellite image. This task is called **batch processing.**

To run the model, select ``Model`` → ``Run Model``.

In the bottom-left corner select ``Run as Batch Process``. That means the processing is not started immediately but is qued (:numref:`Fig41_WQ_Run_As_Batch`)

.. _Fig41_WQ_Run_As_Batch:
.. figure:: /img/3/Fig41_WQ_Run_As_Batch.png

   Sample screenshot.

The **Batch Processing** window opens (:numref:`Fig42_WQ_Batch_Processing_Paramters`).

.. _Fig42_WQ_Batch_Processing_Paramters:
.. figure:: /img/3/Fig42_WQ_Batch_Processing_Paramters.png

   Sample screenshot.

Select ``Sentinel-2`` → ``Autofill`` → ``Select from open layers``. In the ``Multiple selection`` window, select ``Select All`` and click the button ``OK`` (:numref:`Fig43_WQ_Select_Images`).

.. _Fig43_WQ_Select_Images:
.. figure:: /img/3/Fig43_WQ_Select_Images.png

   Sample screenshot.

We QGIS knows we want to apply the data processing to ALL the Sentinel-2 images listed in (:numref:`Fig44_WQ_Batch_Processing_Paramters_2`).

.. _Fig44_WQ_Batch_Processing_Paramters_2:
.. figure:: /img/3/Fig44_WQ_Batch_Processing_Paramters_2.png

   Sample screenshot.

But QGIS still don’t know how to save the results.

Select ``_Clip.tif`` → ``Autofill`` → ``Calculate by Expression``. In the window ``Expression String Builder`` type (:numref:`Fig45_WQ_Expression_String_Builder`):

concat('[file path]\\', left(@Sentinel2 ,18), '_Chl_clip.tif')

where [file path] is the path where you want to save the data processing results.
.. important:: **Be careful to double-up all the backslashes (“\\”) in the path! (e.g. c:\\exercise\\output\\)**

.. hint:: **What does it means concat('[file path]\\', left(@Sentinel2 ,18), '_Chl_clip.tif')?** |br|
   The ``concat`` command concatenates multiple strings.

Click the button ``OK``.

.. _Fig45_WQ_Expression_String_Builder:
.. figure:: /img/3/Fig45_WQ_Expression_String_Builder.png

   Sample screenshot.

Now, QGIS knows how to save the results (:numref:`Fig46_WQ_Batch_processing_parameters_3`).

.. _Fig46_WQ_Batch_processing_parameters_3:
.. figure:: /img/3/Fig46_WQ_Batch_processing_parameters_3.png

   Sample screenshot.

|br|

.. _Estimate-the-chlorophyll-concentration-in-Lake-Trasimeno:

Estimate the chlorophyll's concentration in Lake Trasimeno
````````````````````````````````````````````````````````````
Click the button ``Run``. QGIS runs the processing workflow for each satellite image and saves the results in the output folder.

Remove all the layer from QGIS and import the outputs of the automatic data processing. Each image describes the map of the estimated chlorophyll concentration. (:numref:`Fig47_WQ_Chl_Concentration_images`) shows an example 

.. _Fig47_WQ_Chl_Concentration_images:
.. figure:: /img/3/Fig47_WQ_Chl_Concentration_images.png

   Sample screenshot.

Order the maps from the most recent (top) to the oldest (bottom) (:numref:`Fig48_WQ_Images_Order`).

.. _Fig48_WQ_Images_Order:
.. figure:: /img/3/Fig48_WQ_Images_Order.png

   Sample screenshot.

Let’s compare the temporal changes of the chlorophyll load.

Right-click on the map estimated for 27 August 2016 (layer **T32TQN_20160827_Chl_Clip**) and select ``Properties`` (:numref:`Fig49_WQ_Chl_Properties`).

.. _Fig49_WQ_Chl_Properties:
.. figure:: /img/3/Fig49_WQ_Chl_Properties.png

   Sample screenshot.

In the left-side panel select **Symbology** and set the following parameters (:numref:`Fig50_WQ_Chl_Symbology`):

- ``Render type:`` set ``Singleband pseudocolor``. *This option colourize the map,*
- ``Band:`` set ``Band 1 (Gray)``,
- ``Min and Max:`` keep the default values,
- ``Interpolation:`` set ``Discrete``. *This option assigns a unique colour to all values included in the same class,*
- ``Color ramp:`` click on the arrow and:

   - Select the color ramp ``RdYIGn``. If the color ramp RdYIGn is not listed, click on ``Expand All Color Ramps``,
   - Click ``Invert Color Ramp``. *This option shows a higher concentration in red and a lower concentration in green,*

- ``Mode:`` set ``Quantile``,
- ``Classes:`` set ``7``. *This option creates 7 ranges of chlorophyll concentration.*

Click the button ``Classify``. Then click the button ``Export color map to file`` and save to disk with file name ``colour_ramp``. Now we can to apply the same colour ramp to all the maps.

.. _Fig50_WQ_Chl_Symbology:
.. figure:: /img/3/Fig50_WQ_Chl_Symbology.png

   Sample screenshot.

Click the button ``Apply`` and then ``OK``. The map now shows chlorophyll concentration values about 55 mg/m3, making Lake Trasimeno on edge between eutrophic and hypereutrophic states in summer (:numref:`Fig52_WQ_Chl_Map`).

.. _Fig52_WQ_Chl_Map:
.. figure:: /img/3/Fig52_WQ_Chl_Map.png

   Sample screenshot.

Now apply the saved color ramp to all the other maps. For each map, right-click on the map, select ``Properties`` and go to the **Symbology** menu (:numref:`Fig53_WQ_Loading_Color_Map`).

Set the ``render type:`` as ``singleband pseudocolor``, click the button ``Load color map from file`` and load the file ``colour_ramp``.

.. _Fig53_WQ_Loading_Color_Map:
.. figure:: /img/3/Fig53_WQ_Loading_Color_Map.png

   Sample screenshot.

Click the button ``Apply`` and ``OK``.

Now all the maps have the same colour ramp, and the eutrophic states can be compared.

|br|

Simple analysis of results
````````````````````````````
Let’s analyze the trophic level dynamics of Lake Trasimeno in summer 2016.

Keep the maps of chlorophyll load estimated for 18 July 2016 (layer **T32TQN_20160718_Chl_Clip**), 4 August 2016 (layer **T32TQN_20160804_Chl_Clip**), 27 August 2016 (layer **T32TQN_20160827_Chl_Clip**), 13 September 2016 (layer **T32TQN_20160913_Chl_Clip**), 26 September 2016 (layer **T32TQN_20160926_Chl_Clip**), and close the other maps.

As done in :ref:`Estimate-the-chlorophyll-concentration-in-Lake-Trasimeno`, right-click on each map and select ``Properties``. In the left-side panel select **Symbology** and set the following parameters (:numref:`Fig54_WQ_Chl_Map`):

- ``Render type:`` set ``Singleband pseudocolor``,
- ``Band:`` set ``Band 1 (Gray)``,
- ``Min and Max:`` keep the default values,
- ``Interpolation:`` set ``Discrete``,
- ``Mode:`` set ``Equal Interval``,
- ``Classes:`` set ``4``.

Double-click and edit the class value, colour and label as shown in :numref:`Fig54_WQ_Chl_Map`.

Click the button ``Export color map to file`` and save to disk with file name ``colour_levels``. Now we can load apply the same colour scheme to all the maps.

.. _Fig54_WQ_Chl_Map:
.. figure:: /img/3/Fig54_WQ_Chl_Map.png

   Sample screenshot.

**18 July 2016** |br|
In mid-July, **the majority of Lake Trasimeno is mesotrophic.** Eutrophic zones are limited to the north and shores (:numref:`Fig55_WQ_Chl_Map`).

.. _Fig55_WQ_Chl_Map:
.. figure:: /img/3/Fig55_WQ_Chl_Map.png

   Sample screenshot.

**4 August 2016** |br|
Two weeks later, **most of Lake Trasimeno is eutrophic.** Only the southern lake is still mesotrophic (:numref:`Fig56_WQ_Chl_Map`).

.. _Fig56_WQ_Chl_Map:
.. figure:: /img/3/Fig56_WQ_Chl_Map.png

   Sample screenshot.

**27 August 2016** |br|
At the end of August, **almost all Lake Trasimeno is eutrophic.** Only a small part of the south-east is still mesotrophic (:numref:`Fig57_WQ_Chl_Map`).

.. _Fig57_WQ_Chl_Map:
.. figure:: /img/3/Fig57_WQ_Chl_Map.png

   Sample screenshot.

**September 2016** |br|
In September, Lake Trasimeno **turns to a stable eutrophic state.** (:numref:`Fig58_WQ_Chl_Map`).

.. _Fig58_WQ_Chl_Map:
.. figure:: /img/3/Fig58_WQ_Chl_Map.png

   Sample screenshot (top: 13 September 2016, bottom: 26 September 2016).

Overall, our results are consistent with the characteristics and habitat of Lake Trasimeno (see :ref:`Study-area`).

|br|

.. _Mapping-crop-types:

Mapping crop types (difficulty: intermediate)
----------------------------------------------

Download the data
````````````````````
.. important:: **DATA FOR THE EXERCISE** |br|
   `Click here to download the data for this exercise (2.5 GB). <https://drive.google.com/file/d/145Lh5o4do7niR6YDtlXOjEMcLI2cpqcI/view?usp=sharing>`_

|br|

The environmental problem
````````````````````````````
Agriculture is highly dependent on the climate. For any crop type, the effect of climate change will depend on the crop’s optimal temperature and water availability for growth and reproduction.

The temperature increase will change farming practices. In some countries, warming could increase productivity or allow farmers to shift to crops that are currently grown in warmer areas. A higher temperature could exceed the crop’s optimum temperature in some other countries, and production will decline.

.. Warning:: **The role of climate change.** |br|
   Overall, climate change may make it difficult to grow crops the same ways and in the same places as in the past.

|br|

Scope of the exercise
````````````````````````
This exercise shows a very simple method to map crop types with satellites.

|br|

Study area
````````````
The study area is Wallonia, the southern and most extensive region of Belgium. The climate is temperate, moderately humid, with an annual rainfall of about 780 mm well distributed over the year. |br|
The soil is loamy and moderately well-drained; thus, it does not require irrigation. The main winter crops are Wheat and Barley, while the main Summer crops are Potatoe, Sugar beet and Maize. Field size ranges from 3 ha to 15 ha.

|br|

Satellite images
`````````````````
The analysis is done using two cloud-free Sentinel-2 images collected in the following dates of Spring-Summer 2018:

- 18 April 2018,
- 27 June 2018.

.. Warning:: The Sentinel-2 images used in this exercise are supplied as atmospherically corrected ``L2A`` products. **THUS, THEY CAN BE USED WITHOUT ANY FURTHER PRE-PROCESSING.**

|br|

Land cover information
````````````````````````
Information on the actual land cover is provided as polygons (shapefiles). Each red polygon in :numref:`Fig1_CROP_Study_area` stands for a crop field with available information on the cultivated crop type.

In the study area are cultivated the following main crops:

- Barley,
- Chicory,
- Wheat,
- Flax (linseed),
- Maize,
- Peas,
- Potato,
- Sugar beet.

.. _Fig1_CROP_Study_area:
.. figure:: /img/3/Fig1_CROP_Study_area.png

   Farmlands in the Wallonia region.

|br|

Methods
````````
The mapping process uses the **Minimum Distance** supervised classification algorithm. The training samples, called *Region Of Interest (ROI)* in QGIS, are extracted from available land cover polygons.

|br|

QGIS set-up
````````````
Open QGIS and select ``New Empty Project`` in the main window (:numref:`Fig2_CROP_New_Project`).

.. _Fig2_CROP_New_Project:
.. figure:: /img/3/Fig2_WQ_New_Project.png

   Sample screenshot.

|br|

.. _Prepare-multiband-files-for-10-meter-satellite-images:

Prepare multiband files for 10-meter satellite images
````````````````````````````````````````````````````````
Open the folder ``S2A_MSIL2A_20180418T104021_N0207_R008_T31UFS_20180418T125356.SAFE`` → ``GRANULE`` → ``L2A_T31UFS_A014734_20180418T104512`` → ``IMG_DATA`` → ``R10m``.

Each 10-meter Sentinel-2’s spectral band is stored as a single file. Now select the spectral bands with 10 m spatial resolution, those file names end with  (:numref:`Fig3_CROP_Band_selection`):

- “..._B02_10m.jp2”,
- “..._B03_10m.jp2”,
- “..._B04_10m.jp2”,
- “..._B08_10m.jp2”.

.. _Fig3_CROP_Band_selection:
.. figure:: /img/3/Fig3_CROP_Band_selection.png

   Sample screenshot.

Import these files in QGIS. In the menu bar open ``Layer`` → ``Data Source Manager`` (:numref:`Fig101_Data_Source_Manager`).

.. _Fig101_Data_Source_Manager:
.. figure:: /img/3/Fig101_Data_Source_Manager.png

   Sample screenshot.

On the left-side menu, select **Raster** (:numref:`Fig102_Import_Raster`).

.. _Fig102_Import_Raster:
.. figure:: /img/3/Fig102_Import_Raster.png

   Sample screenshot.

Select the following parameters:

- ``Source type:`` select ``File (Default option)``,
- ``Source:``

- Click on the three dots ``[...]``, browse to the folder ``S2A_MSIL2A_20180418T104021_N0207_R008_T31UFS_20180418T125356.SAFE`` → ``GRANULE`` → ``L2A_T31UFS_A014734_20180418T104512`` → ``IMG_DATA`` → ``R10m``,
- Select the four images (files “.jp2”),
- Click on ``Open`` (:numref:`Fig103_Select_bands`).

.. _Fig103_Select_bands:
.. figure:: /img/3/Fig103_Select_bands.png

   Sample screenshot.

Click **Add** (:numref:`Fig104_add_bands`).

.. _Fig104_add_bands:
.. figure:: /img/3/Fig104_add_bands.png

   Sample screenshot.

Now create the multiband file. |br|
In QGIS menu bar open the ``Raster`` menu and select ``Miscellaneous`` → ``Merge`` (:numref:`Fig4_CROP_Merge`).

.. _Fig4_CROP_Merge:
.. figure:: /img/3/Fig4_CROP_Merge.png

   Sample screenshot.

In the **merge window** click on the three dots ``[...]`` at the end of the ``Input layers`` parameter (:numref:`Fig5_CROP_Merge_window`).

.. _Fig5_CROP_Merge_window:
.. figure:: /img/3/Fig5_CROP_Merge_window.png

   Sample screenshot.

Select all the layers and click **OK** (:numref:`Fig6_CROP_Merge_band_selection`).

.. Caution:: Be careful to check that files are sorted in the following order: **B02, B03, B04 and B08.** |br|
   If the order is different, the saved image will have the wrong order’s spectral bands, and the image processing will give incorrect results.

.. _Fig6_CROP_Merge_band_selection:
.. figure:: /img/3/Fig6_CROP_Merge_band_selection.png

   Sample screenshot.

Select the following parameters in the **Merge window**:

- ``Grab pseudocolor table from first layer:`` unselected,
- ``Place each input file into a separate band:`` select,
- ``Output data type:`` Float32,
- ``Merged:`` Click on the three dots ``[...]``:

   - Save to File
   - Select the folder where you want to save the image. Use the following file name ``S2_20180418_10m.tif``.

.. _Fig105_Merge_settings_10m:
.. figure:: /img/3/Fig105_Merge_settings_10m.png

   Sample screenshot.

|br|

Prepare multiband files for 20-meter satellite images
````````````````````````````````````````````````````````
Repeat the same data processing done for the 10-meter satellite images, and create multiband files for the 20-meter satellite images.

Remove the open layers from QGIS and open the folder ``S2A_MSIL2A_20180418T104021_N0207_R008_T31UFS_20180418T125356.SAFE`` → ``GRANULE`` → ``L2A_T31UFS_A014734_20180418T104512`` → ``IMG_DATA`` → ``R20m``.

Each 20-meter Sentinel-2’s spectral band is stored as a single file. Now select the spectral bands with 20 m spatial resolution, those file names end with (:numref:`Fig7_CROP_20m_band_selection`):

- “…B02_20m.jp2”,
- “…B03_20m.jp2”,
- “…B04_20m.jp2”,
- “…B05_20m.jp2”,
- “…B06_20m.jp2”,
- “…B07_20m.jp2”,
- “…B8A_20m.jp2”,
- “…B11_20m.jp2”,
- “…B12_20m.jp2”.

.. _Fig7_CROP_20m_band_selection:
.. figure:: /img/3/Fig7_CROP_20m_band_selection.png

   Sample screenshot.

Now create the multiband file by merging together the spectral bands, as described in :ref:`Prepare-multiband-files-for-10-meter-satellite-images`.

.. Caution:: Be careful when selecting the input layers. Band **B8A** is the last entry by default. **IT MUST BE MOVED AFTER BAND B07** (:numref:`Fig8_CROP_20m_wrong_band_order`).

.. _Fig8_CROP_20m_wrong_band_order:
.. figure:: /img/3/Fig8_CROP_20m_wrong_band_order.png

   Sample screenshot.

Once band **B8A** is moved AFTER band B07, the list will look like :numref:`Fig9_CROP_20m_correct_band_order`).

.. _Fig9_CROP_20m_correct_band_order:
.. figure:: /img/3/Fig9_CROP_20m_correct_band_order.png

   Sample screenshot.

Select the following parameters in the **Merge window**:

- ``Grab pseudocolor table from first layer:`` unselected,
- ``Place each input file into a separate band:`` select,
- ``Output data type:`` Float32,
- ``Merged:`` Click on the three dots ``[...]``:
- ``Save to File: `` Save the output file as ``S2_20180418_20m.tif`` in the same folder used for 10-meters Sentinel-2 images.

.. _Fig106_Merge_Settings_20m:
.. figure:: /img/3/Fig106_Merge_Settings_20m.png

   Sample screenshot.

|br|

.. _Resize-the-image:

Resize the image
`````````````````
The Sentinel-2 images cover a larger area than our study area. Thus, we can resize them before starting the classification process.

In the menu bar select ``Layer`` → ``Data Source Manager`` (:numref:`Fig107_Data_Source_Manager_Vector`).

.. _Fig107_Data_Source_Manager_Vector:
.. figure:: /img/3/Fig107_Data_Source_Manager_Vector.png

   Sample screenshot.

In the left-side menu select **Vector** and set the following parameters (:numref:`Fig109_Add_Vector`):

- ``Source Type:`` set ``File (Default setting)``,
- ``Source:`` Click on the three dots ``[...]`` and browse to the folder ``Study_area\``. Select the file ``Wallonia_Study_Area.shp`` (:numref:`Fig108_Select_Study_Area_Layer`).

Click the button ``Add``.

.. _Fig109_Add_Vector:
.. figure:: /img/3/Fig109_Add_Vector.png

   Sample screenshot.

.. _Fig108_Select_Study_Area_Layer:
.. figure:: /img/3/Fig108_Select_Study_Area_Layer.png

   Sample screenshot.

A rectangle will appear in the bottom left corner of the image (:numref:`Fig110_Study_Area_Visualization`). This is the extent of the study area.

.. _Fig110_Study_Area_Visualization:
.. figure:: /img/3/Fig110_Study_Area_Visualization.png

   Sample screenshot.

To resize (i.e. clip) the satellite image, search in the **Processing Toolbox** panel the command *clip* and open the tool *Clip raster by mask layer* in the GDAL package (:numref:`Fig111_Clip_tool`).

.. hint:: If the Processing Toolbox panel is not loaded, open the QGIS menu ``View`` → ``Panels`` and select ``Processing Toolbox``.
.. _Fig111_Clip_tool:
.. figure:: /img/3/Fig111_Clip_tool.png

   Sample screenshot.

In the **Clip Raster by Mask Layer** window, set the following parameters (:numref:`Fig112_Clip_tool_Settings`):

- ``Input layer:`` set ``S2_20180418_20m``,
- ``Mask layer:`` set ``Wallonia_Study_Area``,
- ``Source CRS:`` Not set,
- ``Target CRS:`` Not set,
- ``Assign a specified nodata value to output bands:`` Not set,
- ``Create an output alpha band:`` unselect,
- ``Match the extent of the clipped raster to the extent o the mask layer:`` select,
- ``Keep resolution of input raster:`` select,
- ``Set output file resolution``: unselect,
- ``X Resolution of output bands``: Not set,
- ``Y Resolution of output bands``: Not set,
- ``Clipped (mask):`` Click on the three dots [...]. Select ``Save to file`` and browse to the folder where you saved the merged images. Now save the new resized (clipped) image the file name ``S2_20180418_20m_clip``.

Click the button ``RUN``.

.. _Fig112_Clip_tool_Settings:
.. figure:: /img/3/Fig112_Clip_tool_Settings.png

   Sample screenshot.

The new clipped image will appear in QGIS (:numref:`Fig113_Clipped_image`). Now the image is smaller; thus, the subsequent data processing will be faster.

.. _Fig113_Clipped_image:
.. figure:: /img/3/Fig113_Clipped_image.png

   Sample screenshot.

Remove all the layers from QGIS.

|br|

Create the training samples for image classification
`````````````````````````````````````````````````````
In our study area, farmlands are much more extensive than 20 m x 20 m. Thus, we use the 20-meters Sentinel-2 image to perform the classification process. On the one hand we do not need greater detail, and on the other hand the 20-meters images have much more spectral bands, thus allowing a better recognition of crop types.

Import in QGIS the Sentinel-2 multiband image of 27 June 2018 from the folder ``..\Sentinel-2\20m`` (:numref:`Fig114_Import_Clipped_Image`). This image is already merged and resized as described in :ref:`Prepare-multiband-files-for-10-meter-satellite-images` and :ref:`Resize-the-image`.

.. _Fig114_Import_Clipped_Image:
.. figure:: /img/3/Fig114_Import_Clipped_Image.png

   Sample screenshot.

Import in QGIS the shapefile ``Wallonia_2018_In_Situ_Extracted_v1.shp`` that describes a field with available information on the cultivated crop type. This information is stored in the attribute table (:numref:`Fig10_CROP_Dataset_attribute_table`). |br|
To see the attributes, right-click the layer ``Wallonia_2018_In_Situ_Extracted_v1.shp`` and select ``Open Attribute Table``.

.. _Fig10_CROP_Dataset_attribute_table:
.. figure:: /img/3/Fig10_CROP_Dataset_attribute_table.png

   Sample screenshot.

The attribute **LC** (i.e. land cover) describes the crop type, and the attribute **Class_code** assigns a unique numerical code to each land cover class. The database uses the coding scheme of :numref:`Tab1_CROP`.

.. _Tab1_CROP:
.. table:: Land cover classes and class code numbering.

   ===============  ==========
   Land cover       Class code
   ===============  ==========
   Barley           1
   Chicory          2
   Common wheat     3
   Flax (Linseed)   4
   Grassland        5
   Maize            6
   Not Agriculture  7
   Peas             8
   Potato           9
   Sugar beet       10
   ===============  ==========

.. important:: We need some *a priori* information on the land cover for EACH crop type we want to map. This information is used as training samples during the classification process.

Now we have to tell the software which satellite image we want to classify (:numref:`Fig11_CROP_Define_band_set`). |br|
Open the **SCP** tool window. |br|
Select **Band set** from the left-side menu. |br|
Set the parameter ``Multiband image list`` to the Sentinel-2 multiband image ``S2_20180627_20m``.

.. _Fig11_CROP_Define_band_set:
.. figure:: /img/3/Fig11_CROP_Define_band_set.png

   Sample screenshot.

Then we need to convert the shapefile into ROI (Region of Interest) for the classification process to use these polygons as training samples.

Open the **SCP Dock** (:numref:`Fig12_CROP_SCP_Dock_tool`).

.. tip:: If you don’t have the SCP Dock window opened in QGIS, select: ``View`` → ``Panels`` → ``Activate SCP Dock``.

.. _Fig12_CROP_SCP_Dock_tool:
.. figure:: /img/3/Fig12_CROP_SCP_Dock_tool.png

   Sample screenshot.

Open the tab ``Training input`` and click on the icon **Create a new ROI file** (:numref:`Fig13_CROP_Create_new_ROI_file`).

.. _Fig13_CROP_Create_new_ROI_file:
.. figure:: /img/3/Fig13_CROP_Create_new_ROI_file.png

   Sample screenshot.

Select the folder where you want to save the training samples file and name it ``Training``.

Open the main SCP window again and go to the panel ``Basic Tools panel`` → ``Import signatures`` (:numref:`Fig14_CROP_Import_signature`).

.. _Fig14_CROP_Import_signature:
.. figure:: /img/3/Fig14_CROP_Import_signature.png

   Sample screenshot.

and click the button ``Import vector`` (:numref:`Fig15_CROP_Signature_from_vector`)

.. _Fig15_CROP_Signature_from_vector:
.. figure:: /img/3/Fig15_CROP_Signature_from_vector.png

   Sample screenshot.

Now open the shapefile ``Wallonia_2018_In_Situ_Extracted_v1.shp`` (:numref:`Fig16_CROP_Select_the_vector_file`). |br|
The software shows the following information:

- ``MC ID field`` (i.e. Macro Class ID field): this field requires a numerical code to identify the classes we want to classify. QGGIS allows to use an attribute of the shapefile; thus we use the **Class_code**,
- ``MC Name field`` (i.e. Macro Class Name field): this field requires the class name linked with the **MC ID field**. The attribute containing the class name is **LC**,
- In this exercise, we will not use the fields ``C ID`` (i.e. Class ID) and ``C Name`` (i.e. Class Name). Thus, select the same attributes of the Macro Classes.

.. _Fig16_CROP_Select_the_vector_file:
.. figure:: /img/3/Fig16_CROP_Select_the_vector_file.png

   Sample screenshot.

Click the ``Import vector`` icon (:numref:`Fig17_v2_CROP_ROI_Creation`).

.. _Fig17_v2_CROP_ROI_Creation:
.. figure:: /img/3/Fig17_v2_CROP_ROI_Creation.png

   Sample screenshot.

.. important:: Wait until the importing is finished! |br|
   This process might take some minutes, depending on your PC performances.

|br|

Automatic mapping of crop types
````````````````````````````````
Let’s start the classification process.

Open the ``SCP window`` and go to the ``Band processing`` panel. Select ``Classification`` and set the parameters as follows (:numref:`Fig18_CROP_Classification_tool`):

- ``Select input band set:`` set **1**. We set earlier the Sentinel-2 multiband image ``S2_20180627_20m`` as the band set 1,
- ``Use:`` flag **MC ID**. We set earlier the crop type as ``MC ID``,
- ``Algorithm:`` select **Minimum Distance**. We use the minimum distance classification algorithm,
- ``Threshold:`` set **0**. We are telling the algorithm to classify all the image pixels.

.. _Fig18_CROP_Classification_tool:
.. figure:: /img/3/Fig18_CROP_Classification_tool.png

   Sample screenshot.

Click the button ``RUN`` and select the folder where you want to save the classification map. Name the file ``20180627_Classification`` (:numref:`Fig115_Save_Classification`).

.. _Fig115_Save_Classification: 
.. figure:: /img/3/Fig115_Save_Classification.png

   Sample screenshot.

The data processing transforms the input satellite image into a land cover map of crops types. Each pixel of the map is coded with its **Class_code** (:numref:`Tab1_CROP`). All the image pixels whose land cover is not recognized are assigned the **"special" Class_code 0** (unclassified). :numref:`Fig19_CROP_Classification_result` shows the result.

.. _Fig19_CROP_Classification_result:
.. figure:: /img/3/Fig19_CROP_Classification_result.png

   Sample screenshot.

|br|

Simple analysis of results
````````````````````````````
If we want to estimate the most farmed crop, right-click on the classification layer ``20180627_Classification`` and select ``Properties`` (:numref:`Fig20_CROP_Classification_properties`).

.. _Fig20_CROP_Classification_properties:
.. figure:: /img/3/Fig20_CROP_Classification_properties.png

   Sample screenshot.

In the left-side menu select ``Histogram`` and then click the button ``Compute Histogram``. |br|
This tool counts the number of pixels for each land cover class, called **frequency** (:numref:`Fig21_CROP_Classification_histogram`). |br|
We see that the crop Flax (Linseed), *coded with the class number 4*, is the most farmed in the study area.

.. _Fig21_CROP_Classification_histogram:
.. figure:: /img/3/Fig21_CROP_Classification_histogram.png

   Sample screenshot.

.. hint:: If we have some information on the land cover and satellite images for the same location, but in a different period, we can compare how the farming of crop types changes in time.

.. hint:: If we have some information on the land cover and satellite images for the same period, but in a different location, we can compare how crop types are farmed in other places.

|br|

.. _Monitoring-crops-vegetative-stage:

Monitoring crops’ vegetative stage (difficulty: easy)
------------------------------------------------------

Download the data
````````````````````
.. important:: **DATA FOR THE EXERCISE** |br|
   `Click here to download the data for this exercise (270 MB). <https://drive.google.com/file/d/1iyZDXhl4NnlTixUk2BVecHNT6q2uJd0u/view?usp=sharing>`_

|br|

.. _The-environmental-problem-agricultural-productivity:

The environmental problem
````````````````````````````
Agricultural productivity is strictly related to environmental factors. For example:

- Rising levels of CO2 reduce protein content and essential minerals in most crops, including Wheat, Soybeans, and Rice, resulting in a loss of food quality,
- Extreme temperature and precipitation can prevent crops from growing,
- Floods and droughts can harm crops and reduce productivity,
- Droughts can cause desertification,
- Many insects and fungi prosper under warmer temperatures, wetter climates, and increased CO2 levels,
- Pollutants reduce agricultural productivity.

.. Warning:: **The role of climate change** |br|
   Climate change is modifying the temperature and the precipitation regimes, intensifying extreme weather, and increasing desertification in many fragile territories. That has an impact on the health of vegetation and crops.

|br|

Scope of the exercise
````````````````````````
This exercise shows satellites’ use to evaluate Barley and Potatoes’ vegetative stage in different periods of the year.

|br|

Study area
````````````
The study area is Wallonia, the southern and most extensive region of Belgium. The climate is temperate, moderately humid, with an annual rainfall of about 780 mm well distributed over the year. |br|
The soil is loamy and moderately well-drained; thus, it does not require irrigation. The main winter crops are Wheat and Barley, while the main Summer crops are Potatoe, Sugar beet and Maize. Field size ranges from 3 ha to 15 ha.

|br|

Satellite images
`````````````````
The analysis is done using two cloud-free Sentinel-2 images collected in the following dates of Spring-Summer 2018:

- 18 April 2018,
- 27 June 2018.

.. Warning:: The Sentinel-2 images used in this exercise are supplied as atmospherically corrected ``L2A`` products. **THUS, THEY CAN BE USED WITHOUT ANY FURTHER PRE-PROCESSING.**

|br|

Land cover information
````````````````````````
Information on the actual land cover is provided as polygons (shapefiles). Each red polygon in :numref:`Fig1_NDVI_Study_area` stands for a crop field with available information on the cultivated crop type.

In the study area are cultivated the following main crops:

- Barley,
- Chicory,
- Wheat,
- Flax (linseed),
- Maize,
- Peas,
- Potato,
- Sugar beet.

.. _Fig1_NDVI_Study_area:
.. figure:: /img/3/Fig1_CROP_Study_area.png

   Farmlands in the Wallonia region.

|br|

Methods
`````````
The monitoring of vegetative stage is done using the **Normalized Difference Vegetation Index (NDVI)** (:ref:`Examples-of-spectral-indices-for-studying-vegetation`) described by Equation :eq:`eqSI2`:

.. math:: NDVI=\frac{\rho_{NIR}-\rho_{Red}}{\rho_{NIR}+\rho_{Red}}

|br|

QGIS set-up
````````````
Open QGIS and select ``New Empty Project`` in the main window (:numref:`Fig2_NDVI_New_Project`).

.. _Fig2_NDVI_New_Project:
.. figure:: /img/3/Fig2_WQ_New_Project.png

   Sample screenshot.

|br|

.. _Calculate-NDVI:

Calculate NDVI
````````````````
To compute NDVI, we need only the NIR and Red bands. Thus, we use Sentinel-2’s highest spatial resolution images (10-meters).

Open the folder ``…\Sentinel-2\10m`` and import in QGIS the image ``S2_20180418_10m``.

.. note:: Prepare the input multiband satellite images as described in :ref:`Prepare-multiband-files-for-10-meter-satellite-images`.

Now we do some calculations with images using the **Raster Calculator**. This tool allows evaluating equations based on the image pixel values. |br|
Open **Raster Calculator** from the menu ``Raster`` → ``Raster Calculator...`` (:numref:`Fig1_NDVIRaster_calculator`).

.. _Fig1_NDVIRaster_calculator:
.. figure:: /img/3/Fig1_NDVI_Raster_calculator.png

   Sample screenshot.

We want to calculate the NDVI for each of the satellite image pixels (for more information refer to :ref:`Examples-of-spectral-indices-for-studying-vegetation`):

.. math:: NDVI=\frac{\rho_{NIR}-\rho_{Red}}{\rho_{NIR}+\rho_{Red}}

Before writing the calculation formula for NDVI, we need to know which are the Red and NIR spectral bands. |br|
Remember that Sentinel-2’s 10-meters resolution Red band is band 3 (B3), and its 10-meters resolution NIR band is band 4 (B4). Thus, the NDVI equation written for Sentinel-2 images becomes Equation :eq:`eqNDVI1`:

.. math:: NDVI=\frac{\rho_{Band\ 4}-\rho_{Band\ 3}}{\rho_{Band\ 4}+\rho_{Band\ 3}}
   :label: eqNDVI1

Equation :eq:`eqNDVI1` can also be written as follows:

.. math:: NDVI=(B4-B3)/(B4+B3)
   :label: eqNDVI2

where: |br|
B3 are the pixel values in Band 3 (i.e. the Red band), |br|
B4 are the pixel values in Band 4 (i.e. the NIR band).

Now, we have to write Equation :eq:`eqNDVI2` using QGIS syntax, so the software can understand it. |br|
With the help of the calculator buttons, write the following expression in ``Raster Calculator Expression``:

("S2A_20180418_10m@4" - "S2A_20180418_10m@3")/("S2A_20180418_10m@4"+"S2A_20180418_10m@3")

.. hint:: **How to read QGIS equations?**

   "S2A_20180418_10m@4" means: |br|
   *“pick each pixel value of image S2A_20180418_10m for band 4 (@4)”*.

   "S2A_20180418_10m@3" means: |br|
   *“pick each pixel value of image S2A_20180418_10m for band 3 (@3)”*.

   **Equations are calculated on a pixel basis. Thus the same equation is computed for each image pixel individually. The results are shown in a new image.**

In **Result Layer** click on the three dots ``[...]`` next to ``Output layer`` and select where you want to save the classification results. Name the folder ``..\NDVI`` and the file ``2018_04_18_NDVI``  (:numref:`Fig2_NDVI_Raster_Calculator_window`).

.. _Fig2_NDVI_Raster_Calculator_window:
.. figure:: /img/3/Fig2_NDVI_Raster_Calculator_window.png

   Sample screenshot.

The output is a grayscale image, where each pixel contains its NDVI value just computed (:numref:`Fig3_NDVI_April_NDVI`).

.. _Fig3_NDVI_April_NDVI:
.. figure:: /img/3/Fig3_NDVI_April_NDVI.png

   Sample screenshot.

Now repeat the data processing again for the satellite image collected on 27 June 2018 (multiband file ``S2_20180627_10m``). |br|
Remember to use **"S2A_20180627_10m@3"** and **"S2A_20180627_10m@4"** in the expression for calculating NDVI on 27 June 2018. Save results as ``..\NDVI\2018_06_27_NDVI``.

.. tip:: To simplify the processing, remove all the layer from QGIS and start from scratch (:ref:`Calculate-NDVI`).

|br|

Select the NDVI information for Barley and Potato
````````````````````````````````````````````````````
Once computed the NDVI for both the satellite images, we want to compare Barley and Potato’s vegetative stage in April and June.

Open the attribute table of the shapefile **Wallonia_2018_In_Situ_Extracted_v1**: right-click on ``Wallonia_2018_In_Situ_Extracted_v1`` → ``Open Attribute Table`` (:numref:`Fig4_NDVI_Open_Attribute_table`).

.. _Fig4_NDVI_Open_Attribute_table:
.. figure:: /img/3/Fig4_NDVI_Open_Attribute_table.png

   Sample screenshot.

To filter the attribute table by land cover type (the attribute **LC**), we need the tool **Select feature using an expression.** Click the icon showed in (:numref:`Fig5_NDVI_Select_by_expression`).

.. _Fig5_NDVI_Select_by_expression:
.. figure:: /img/3/Fig5_NDVI_Select_by_expression.png

   Sample screenshot.

The window **Select by Expression** opens. Expand the tree **Fields and Values** and double click on ``LC`` (:numref:`Fig6_NDVI_select_LC`).

.. _Fig6_NDVI_select_LC:
.. figure:: /img/3/Fig6_NDVI_select_LC.png

   Sample screenshot.

The main window **Expression** automatically fills with “LC”. |br|
Click the button ``=`` and then click the button ``All Unique``. This command shows, on the right side, the list of all available land cover in the shapefile **Wallonia_2018_In_Situ_Extracted_v1**. |br|
Double click on ``Barley (winter)``. Now the expression in the main window becomes "LC" =  'Barley (winter)' (:numref:`Fig7_NDVI_Select_Barley`).

.. _Fig7_NDVI_Select_Barley:
.. figure:: /img/3/Fig7_NDVI_Select_Barley.png

   Sample screenshot.

We are telling the software to select the land cover Barley. But we want to select also Potato. |br|
Expand the tree **Operators** and double click on the **OR** operator (:numref:`Fig8_NDVI_Select_OR_operator`).

.. _Fig8_NDVI_Select_OR_operator:
.. figure:: /img/3/Fig8_NDVI_Select_OR_operator.png

   Sample screenshot.

Expand the tree **Fields and Values** again, double click **LC**, click the button ``=`` and then click the button ``All Unique``. Now double click on ``Potato``.

The expression in the main window becomes "LC"  =  'Barley (winter)'  OR  "LC"  =  'Potato (non-early)' (:numref:`Fig9_NDVI_Select_Potato`). We are now telling the software to select from the attribute table all the polygons whose land cover is Barley or Potato.

.. _Fig9_NDVI_Select_Potato:
.. figure:: /img/3/Fig9_NDVI_Select_Potato.png

   Sample screenshot.

Click the button **Select Features** (bottom right of the window) and then **Close** the window.

As a result, 13 polygons out of 55 are selected. Now export these polygons in a new layer. Right-click on the layer name → ``Export`` → ``Save Selected Features As...`` (:numref:`Fig10_NDVI_Export_Selected_Features`).

.. _Fig10_NDVI_Export_Selected_Features:
.. figure:: /img/3/Fig10_NDVI_Export_Selected_Features.png

   Sample screenshot.

A window opens. Select the following parameters (:numref:`Fig11_NDVI_Save_Vector_Layer_as`):

- ``Format:`` set to ``ESRI Shapefile``,
- ``File name:`` Double-click on the three dots ``[...]`` and select the folder where you want to save the file. Name it: ``Barley_Potato``,
- ``Layer name:`` Leave this field empty,
- ``CRS:`` Keep the default value. QGIS automatically takes the Coordinate Reference System (CRS) of the original file.
- Keep the default values for the other parameters.

.. _Fig11_NDVI_Save_Vector_Layer_as:
.. figure:: /img/3/Fig11_NDVI_Save_Vector_Layer_as.png

   Sample screenshot.

|br|

Compare winter crops and summer crops
````````````````````````````````````````
Now we want to compare the different vegetative stage of Barley and Potato. For this task, we use the **Zonal statistics** tool. |br|
Unlike the **Cell Statistics** algorithm that computes per-pixel statistics, the **Zonal statistics** algorithm calculates per-polygon statistics. That means the output (e.g. minimum, maximum, sum, count, *etc.*) is calculated only on pixels within the selected polygons.

Search in the **Processing Toolbox** panel for the **Zonal statistics** (or write *zonal statistics* in the Processing Toolbox search bar) and double-click on it (:numref:`Fig11_NDVI_Zonal_Statistics`).

.. hint:: If the Processing Toolbox panel is not loaded, open the QGIS menu ``View`` → ``Panels`` and select ``Processing Toolbox``.

.. _Fig11_NDVI_Zonal_Statistics:
.. figure:: /img/3/Fig11_NDVI_Zonal_Statistics.png

   Sample screenshot.

The Zonal Statistics window opens. Select the following parameters (:numref:`Fig12_NDVI_Zonals_Statistics_Parameters`): 

- **Input layer:** set ``Barley_Potato``,
- **Raster layer:** set to ``2018_04_18_NDVI``,
- **Raster band:** set to ``Band 1 (Gray)``,
- **Output column prefix:** set to ``18_04_``,
- Statistics to calculate:

   - Click on the three dots ``[...]``,
   - Select **Mean** and unselect all the other statistics,
   - Click the blue back arrow, located in the upper-left corner (:numref:`Fig13_NDVI_Zonal_statistics_select_mean`).

- Zonal Statistics:

   - Click on the three dots ``[...]``,
   - Save to file,
   - Select the folder where to save the Zonal Statistics file,
   - Name the file ``Zonal_statistics_18_04``.

Click the button ``RUN`` to execute the data processing.

.. _Fig12_NDVI_Zonals_Statistics_Parameters:
.. figure:: /img/3/Fig12_NDVI_Zonals_Statistics_Parameters.png

   Sample screenshot.

.. _Fig13_NDVI_Zonal_statistics_select_mean:
.. figure:: /img/3/Fig13_NDVI_Zonal_statistics_select_mean.png

   Sample screenshot.

The data processing adds a new shapefile layer, called ``b4_b3_mean``. This is a copy of the shapefile ``Sampling_2016`` with the new attribute (i.e. column) ``b4/b3_mean``. The new attribute ``b4/b3_mean`` contains the mean RVI of each polygon (i.e. rows) (:numref:`Fig14_NDVI_18_April_NDVI_in_the_attribute_table`).

.. _Fig14_NDVI_18_April_NDVI_in_the_attribute_table:
.. figure:: /img/3/Fig14_NDVI_18_April_NDVI_in_the_attribute_table.png

   Sample screenshot.

Now compute the zonal statistics for the satellite image collected on 27 June 2018 (file ``2018_06_27_NDVI``).
Remember to set the **Raster layer** to ``2018_06_27_NDVI``, and **Output column prefix:** to ``27_06_``. |br|
:numref:`Fig15_NDVI_27_June_NDVI_in_the_attribute_table` shows the result.

.. _Fig15_NDVI_27_June_NDVI_in_the_attribute_table:
.. figure:: /img/3/Fig15_NDVI_27_June_NDVI_in_the_attribute_table.png

   Sample screenshot.

|br|

Simple analysis of results
````````````````````````````
Let’s discuss our findings.

- **Mid April:**

   - **Barley has high NDVI values**, corresponding to a high amount of healthy biomass (just before harvesting),
   - **Potato has low NDVI values**, corresponding to a low biomass amount (because the seedling is not grown yet).

- **Late June:**

   - **Barley has low NDVI values**, corresponding to a low biomass amount (because the crop has been harvested),
   - **Potato has high NDVI values**, corresponding to a high amount of healthy biomass (because the crop grew up).

We thus **deduce** that *Barley is cultivated as a winter crop* in the study area. |br|
In contrast, we **deduce** that *Potato is cultivated as a summer crop* in the study area.

.. note::

   It is interesting to notice that, unlike one may expect, not all the fields with the same crop have the same NDVI values in the period of full growth. This phenomenon is easily explained because the seedlings’ health and vigour may vary due to non-optimal environmental conditions.

   Thus, fields cultivated with Barley in winter, or fields cultivated with Potato in summer, showing abnormal low NDVI values could have productivity issues related to environmental factors, as recalled in :ref:`The-environmental-problem-agricultural-productivity`.

|br|
|br|

Additional resources
---------------------
For additional hands-on, have a look at the following recommended practices by the `United Nations Office for Outer Space Affairs <https://un-spider.org/>`_ using QGIS and open data:

- `Flood mapping and damage assessment <https://un-spider.org/advisory-support/recommended-practices/flood-mapping-and-damage-assessment-using-s2-data/step-by-step>`_ using Sentinel-2 data (UN-SPIDER).
- Use of digital elevation data for `storm surge coastal flood modelling <https://un-spider.org/advisory-support/recommended-practices/dem-storm-surge-coastal-monitoring-airbus>`_ (UN-SPIDER).
- `Disaster preparedness <https://un-spider.org/advisory-support/recommended-practices/recommended-practice-disaster-preparedness-software-extensions/step-by-step-overview>`_ using free software extensions (UN-SPIDER).
- `Exposure Mapping <https://un-spider.org/advisory-support/recommended-practices/recommended-practice-exposure-mapping>`_ (UN-SPIDER).

|br|

(v.11.03.20-10.15)