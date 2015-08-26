.. _geonode_create_layer:


################
Creating a Layer
################

Layers are a published resource representing a raster or vector spatial data source. 
Layers also can be associated with metadata, ratings, and comments.

You can create new layers using the GeoNode web interface.
Without being logged in, you are limited to read-only access of public layers, 
since data upload is only enabled for registered user.

1. If you are not logged in yet, sign in.

2. Press the "upload" btton in the toolbar:
 
   .. image:: img/geonode_toolbar.png

3. You will be presented with a page where you can choose which kind of resource you are going to create:

   .. image:: img/geonode_upload.png

   Press the "Upload geographic data" button.
   

4. You will be presented a page that tells you there are a few steps to be performed 
   for publishing a layer:
   
   - upload data
   - edit layer's metadata
   - review your input
   
   .. image:: img/C-READ_UpLoadLayers1.png

   The left column also explains what is needed to be done in each step.

   This page requires the user to choose and upload the data.
   You can upload either :
   
   - a shapefile (a set of a ``.dbf``, a ``.shp``, a ``.prj``, and an optional ``.xml`` file)
   - a zipped shapefile (a set of the previously described files, compressed in a single ``.zip`` file;
   - a GeoTiff file.

   You have two possibilities to add your files: you can either do that by using drag & drop 
   or you choose to browse them. 
   Be aware that you have to upload a complete set of files, 
   consisting of a shp, a prj, a dbf and a shx file. 
   If one of them is missing,  GeoNode will warn you and you will have to 
   provide the full file set before you can upload them.

   Once you have provided the file(s) you want to ingest, press the "Upload" button at the bottom
   of the page.
   
   You'll get a progress bar while uploading. 
   
   .. image:: img/geonode_upload_progress.png
   
   When the upload is finished, you will be able to go
   on by pressing the "Next" button.
   
   .. image:: img/geonode_layer_upload_complete.png
    

4. Edit the required metadata.

   The C-READ system only requires a minimal set of metadata, that is:
   
   - Title
   - Abstract
   - C-READ category/subcategory

   .. figure:: img/C-READ_EditMetadata.png

      Edit Metadata page

   
   Once these fields are set, you may go on on the next page by pressing the "Next" button.
   
   Anyway, if you have some more metadata to add to the resource, you may press the "Advanced"
   button.

5. Optionally edit the Advanced Metadata.

   .. figure:: img/C-READ_EditMetadataAdvance.png
   
   Advanced metedata (excerpt)

   Taking a closer look on to the advanced metadata, you can see this list of fields:

   * Owner
   * Date
   * Data type
   * Edition
   * Purpose
   * Maintenance frequency
   * Keywords region
   * Restrictions
   * Restrictions other
   * Language
   * Topic Category
   * Spatial representation type
   * Temporal extent start
   * Temporal extent end
   * Supplemental information
   * Distribution URL
   * Distribution description
   * Data quality statement
   * Keywords
   * Point of contact
   * Metadata author
   
   This is a set of information that are loosely coupled with the mandatory metadata 
   of the ISO19115 metadata standard (a standard for geogrphic metadata);
   Anyway in the C-READ context these information may be skipped.
   Some fields will be automatically compiled by the system: for instance. the ISO19115 
   Topic Category field is inferred from the C-READ subcategory; you may anyway modify the 
   inferred value to a new one.  

   If you are creating a vector layer, you will also the grid
   
   * Attributes (those can though not be changed!)

   When finished click the "Update" button at the bottom 
   to update metadata and pass to the next page.
   
6. Review your information

   After you save the layer metadata, you will be brought to the layer details page.
   
   .. figure:: img/geonode_layer_details.png
   
   Layer details page
       
   You can see that your layer is still **unpublished**. 
   You have to wait for an administrator to review the data and metadata you entered. 
   If the administrator is satisfied with your data, the layer will be published. 
   The new resource will be visible to other users only after the admin will have published it.         


==========
Edit style
==========

Edit style task can be performed only by the user who have the permission to do it.

1. In the Explore Layer page choose a Layer that you want to edit clicking over the name of layer or in the preview window.

2. In the Edit Layers page click the Edit Layer button.

3. In the Edit Layer window click Edit button under Style icon. In this interface is it possible to change the style of layers. C-READ GeoNode allows to edit layer styles graphically, without the need to resort to programming or requiring a technical background.

In the following example the layer has one style and one rule in that style. Click *Edit* in Styles menu change Title and Abstract of the selected Style.

.. image:: img/C-READ_LayerStyles.png

Layer Styles window

.. image:: img/C-READ_LayerStyles_UserStyle.png

User Styles window

Click the Rule (Untitled 1) to select it, and then click on *Edit* below it. Edit the style choosing Basic tab to edit symbology of layers, Labels to add and manage labels and Advanced to manage styles by scale and condition. When done, click *Save*, then click on the word Layers to return to the layer list.


.. image:: img/C-READ_StyleRuleBasic.png

Basic Style Rule window

.. image:: img/C-READ_StyleRuleLabel.png

Labels Style Rule windows

.. image:: img/C-READ_StyleRuleAdvanced.png

Advanced Style Rule windows

4. In the Edit Layer window click Manage button under Style icon.
Manage Styles function allows to assign available style to selected layers.

.. image:: img/C-READ_ManageStyles.png
