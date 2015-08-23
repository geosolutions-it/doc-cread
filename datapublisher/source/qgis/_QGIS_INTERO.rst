.. _QGIS_intero:


########
Overview
########

QGIS is an Open Source Geographic Information System. The project was born in May of 2002 and was established as a project on SourceForge in June of the same year. We’ve worked hard to make GIS software (which is traditionally expensive proprietary software) a viable prospect for anyone with basic access to a personal computer. QGIS currently runs on most Unix platforms, Windows, and OS X. QGIS is developed using the Qt toolkit (http://qt.digia.com) and C++. This means that QGIS feels snappy and has a pleasing, easy-to-use graphical user interface (GUI).

QGIS aims to be a user-friendly GIS, providing common functions and features. The initial goal of the project was to provide a GIS data viewer. QGIS has reached the point in its evolution where it is being used by many for their daily GIS data-viewing needs. QGIS supports a number of raster and vector data formats, with new format support easily added using the plugin architecture.

QGIS is released under the GNU General Public License (GPL). Developing QGIS under this license means that you can inspect and modify the source code, and guarantees that you, our happy user, will always have access to a GIS program that is free of cost and can be freely modified. You should have received a full copy of the license with your copy of QGIS, and you also can find it in Appendix GNU General Public License.


========
Features
========
QGIS offers many common GIS functionalities provided by core features and plugins. A short summary of six general categories of features and plugins is presented below, followed by first insights into the integrated Python console.

View data
---------
You can view and overlay vector and raster data in different formats and projections without conversion to an internal or common format. Supported formats include:

- Spatially-enabled tables and views using PostGIS, SpatiaLite and MS SQL Spatial, Oracle Spatial, vector formats supported by the installed OGR library, including ESRI shapefiles, MapInfo, SDTS, GML and many more.
- Raster and imagery formats supported by the installed GDAL (Geospatial Data Abstraction Library) library, such as GeoTIFF, ERDAS IMG, ArcInfo ASCII GRID, JPEG, PNG and many more.
- GRASS raster and vector data from GRASS databases (location/mapset).
- Online spatial data served as OGC Web Services, including WMS, WMTS, WCS, WFS, and WFS-T.

Explore data and compose maps
-----------------------------

You can compose maps and interactively explore spatial data with a friendly GUI. The many helpful tools available in the GUI include:

- QGIS browser
- On-the-fly reprojection
- DB Manager
- Map composer
- Overview panel
- Spatial bookmarks
- Annotation tools
- Identify/select features
- Edit/view/search attributes
- Data-defined feature labeling
- Data-defined vector and raster symbology tools
- Atlas map composition with graticule layers
- North arrow scale bar and copyright label for maps
- Support for saving and restoring projects

Create, edit, manage and export data
------------------------------------
You can create, edit, manage and export vector and raster layers in several formats. QGIS offers the following:

- Digitizing tools for OGR-supported formats and GRASS vector layers
- Ability to create and edit shapefiles and GRASS vector layers
- Georeferencer plugin to geocode images
- GPS tools to import and export GPX format, and convert other GPS formats to GPX or down/upload directly to a GPS unit (On Linux, usb: has been added to list of GPS devices.)
- Support for visualizing and editing OpenStreetMap data
- Ability to create spatial database tables from shapefiles with DB Manager plugin
- Improved handling of spatial database tables
- Tools for managing vector attribute tables
- Option to save screenshots as georeferenced images
- DXF-Export tool with enhanced capabilities to export styles and plugins to perform CAD-like functions

Analyse data
------------
You can perform spatial data analysis on spatial databases and other OGR- supported formats. QGIS currently offers vector analysis, sampling, geoprocessing, geometry and database management tools. You can also use the integrated GRASS tools, which include the complete GRASS functionality of more than 400 modules. (See section GRASS GIS Integration.) Or, you can work with the Processing Plugin, which provides a powerful geospatial analysis framework to call native and third-party algorithms from QGIS, such as GDAL, SAGA, GRASS, fTools and more.


Publish maps on the Internet
----------------------------
QGIS can be used as a WMS, WMTS, WMS-C or WFS and WFS-T client, and as a WMS, WCS or WFS server. Additionally, you can publish your data on the Internet using a webserver with UMN MapServer or GeoServer installed.

Extend QGIS functionality through plugins
-----------------------------------------
QGIS can be adapted to your special needs with the extensible plugin architecture and libraries that can be used to create plugins. You can even create new applications with C++ or Python!

Core Plugins
^^^^^^^^^^^^
Core plugins include:

1. Coordinate Capture (Capture mouse coordinates in different CRSs)
#. DB Manager (Exchange, edit and view layers and tables; execute SQL queries)
#. Dxf2Shp Converter (Convert DXF files to shapefiles)
#. eVIS (Visualize events)
#. fTools (Analyze and manage vector data)
#. GDALTools (Integrate GDAL Tools into QGIS)
#. Georeferencer GDAL (Add projection information to rasters using GDAL)
#. GPS Tools (Load and import GPS data)
#. GRASS (Integrate GRASS GIS)
#. Heatmap (Generate raster heatmaps from point data)
#. Interpolation Plugin (Interpolate based on vertices of a vector layer)
#. Metasearch Catalogue Client
#. Offline Editing (Allow offline editing and synchronizing with databases)
#. Oracle Spatial GeoRaster
#. Processing (formerly SEXTANTE)
#. Raster Terrain Analysis (Analyze raster-based terrain)
#. Road Graph Plugin (Analyze a shortest-path network)
#. Spatial Query Plugin
#. SPIT (Import shapefiles to PostgreSQL/PostGIS)
#. Topology Checker (Find topological errors in vector layers)
#. Zonal Statistics Plugin (Calculate count, sum, and mean of a raster for each polygon of a vector layer)


External Python Plugins
^^^^^^^^^^^^^^^^^^^^^^^
QGIS offers a growing number of external Python plugins that are provided by the community. These plugins reside in the official Plugins Repository and can be easily installed using the Python Plugin Installer



###############
Installing QGIS
###############

This section gives a quick overview of installing QGIS, some sample data from the QGIS web page, and running a first and simple session visualizing raster and vector layers.

============
Installation
============

Installation of QGIS is very simple. Standard installer packages are available for MS Windows and Mac OS X. For many flavors of GNU/Linux, binary packages (rpm and deb) or software repositories are provided to add to your installation manager. Get the latest information on binary packages at the QGIS website at http://download.qgis.org


Installation from source
------------------------

If you need to build QGIS from source, please refer to the installation instructions. They are distributed with the QGIS source code in a file called INSTALL. You can also find them online at http://htmlpreview.github.io/?https://raw.github.com/qgis/QGIS/master/doc/INSTALL.html

Installation on external media
------------------------------
QGIS allows you to define a configpath option that overrides the default path for user configuration (e.g., ~/.qgis2 under Linux) and forces QSettings to use this directory, too. This allows you to, for instance, carry a QGIS installation on a flash drive together with all plugins and settings.


##########################
Installing workflow plugin
##########################

Processing Workflows is a plugin for QGIS for creating processing workflows. The workflows provide step-by-step instructions and guidance for less experienced users thus facilitating capacity building in Earth observation data analysis and GIS tasks.

QGIS has been designed with a plugin architecture. This allows many new features and functions to be easily added to the application. 
You can manage your plugins in the plugin dialog which can be opened with **Plugins** > **Manage and install plugins**.

.. image:: img/QGIS_PlugIn.png

The menus in the Plugins dialog allow the user to install, uninstall and upgrade plugins in different ways. Each plugin have some metadatas displayed in the right panel:

- information if the plugin is experimental
- description
- rating vote(s) (you can vote for your prefered plugin!)
- tags
- some useful links as the home page, tracker and code repository
- author(s)
- version available

Here, all the available plugins are listed, including both core and external plugins. this menu lists all plugins available that are not installed. Choose Not Installed, in Search function type "Processing Workflows" select it in the list and click Install plugin button to implement it into QGIS.

.. image:: img/QGIS_GestionePlugIn.png

In Settings menu, you can use the following options:

- Check for updates on startup. Whenever a new plugin or a plugin update is available, QGIS will inform you ‘every time QGIS starts’, ‘once a day’, ‘every 3 days’, ‘every week’, ‘every 2 weeks’ or ‘every month’.
- Show also experimental plugins. QGIS will show you plugins in early stages of development, which are generally unsuitable for production use.
- Show also deprecated plugins. These plugins are deprecated and generally unsuitable for production use.

To add external author repositories, click [Add...] in the Plugin repositories section. If you do not want one or more of the added repositories, they can be disabled via the [Edit...] button, or completely removed with the [Delete] button.

.. image:: img/QGIS_SettingsPlugIn.png


#####################
Installing a workflow
#####################

After installing and activating the plugin, it also needs to be activated in Processing options which are accessible from QGIS main menu (Processing > Options and configuration). The path to the directory where the workflow files are stored (by default in the plugin directory) can also be set:

.. image:: img/QGIS_ProcessingOptions.png 


After the activation the workflow library can be accessed through the Processing Toolbox and also from an icon on the QGIS task bar:

.. image:: img/QGIS_WorkFlowLibrary.png

A workflow consists of a number of steps, with each step having an instruction pane on the left and the algorithm window on the right. After a step execution is started (by pressing the Run button) and completed, the next step will automatically open. It is also possible to skip steps without execution and go back to previous steps by using the buttons at the bottom of the workflow dialog:

.. image:: img/QGIS_workflow.png


##################
Running a workflow
##################
New workflows can be easily added by using the Workflow Creator which can be accessed from the Processing Toolbox (Workflows > Tools > Create new workflow). Existing workflows can also be edited by right clicking on them and selecting Edit workflow:

.. image:: img/QGIS_WorkFlowEdit.png

In the Workflow Creator new algorithms can be added to a workflow by double clicking on any algorithm in the list on the left. All algorithms available in the Processing Toolbox, including models and scripts, can be added to a workflow. To remove an algorithm from a workflow the Remove step at the bottom of the dialog should be used. The order of the algorithms can be changed by dragging the tabs with algorithm names at the top of the dialog. To save a workflow its name and group should be entered at the top of the dialog and the save button clicked. Workflows are saved in a text file which contains information on the number and order of steps, the instructions for each step and any pre-set values of numeric, text, drop-down list or boolean algorithm parameters. The workflows can also be tested before saving by using the Test button.

.. image:: img/QGIS_WorkFlowCreator.png



