.. _QGIS:


########
Raster process and publishing workflows
########

Overview
---------

Any raster published on a geospatial server must be optimized in order to be efficently served to the clients

This workflow compute the raster retiling and creates its overviews using GDAL-Translate for the former and GDAL-addo for the latter action (Steps 1, 2)

The optimized layer will be at the end (Step 3) published on Geonode as a single-image Raster Layer

.. image:: img/QGIS_Raster_workflow.png

Step 1/3 - Retile with GDAL translate
---------

Uses GDAL-Translate to perform retiling and improve pan actions on the layer once published

See the `GDAL documentation <http://www.gdal.org/gdal_translate.html>`_  for more info about GDAL translate

**Main Parameters:**

- **Input Vector** Select on the file system the raster to process

Step 2/3 - Add overviews with GDAL addo
---------

Uses GDAL-Addo to create overviews to improve zoom actions of the layer

See the `GDAL documentation <http://www.gdal.org/gdal_translate.html>`_ for more info about GDAL addo

**Main parameters:**

- **Input Vector** Select on the file system the raster to process


Step 3a/3 - Geonode raster publishing as a single layer
---------

Publish the Raster layer created on a Geonode instance

**Main parameters:**

- **Geonode URL** the base URL of the Geonode instance.
	examples:
		``http://192.168.50.170:8000`` or ``http://awebsite.geonode.org``
- **User** a username who has the publications grants required
- **Password** the user password
- **Raster Layer** the previously created layer opened in the current project
- **Title** a geonode metadata
- **Abstact** a geonode metadata

Step 3b/3 - Geonode raster publishing as a imagemosaic  update
---------

Update an Image mosaic with the raster layer created.

The raster will be directly published on  Geoserver , adding a one more time instance to an Imagemosaic datastore

**Main parameters:**

- **Geoserver URL** the base URL of the Geonode instance.
	examples:
		``http://192.168.50.170:8080/geosever`` or ``http://awebsite.geonode.org/geoserver``

- **Image mosaic Store Name** the name of the datastore published on Geoserver
- **Image mosaic Granule to add** the previously created layer opened in the current project
