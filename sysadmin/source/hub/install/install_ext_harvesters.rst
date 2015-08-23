.. _install_ext_harvesters_cread:

###########################
Installing other harvesters
###########################

============
Introduction
============

The CKAN hub will gather informations from different sources.
Among these, we have the main data node based on GeoNode, and the  
CCCCCC ClearingHouse.

.. _install_ext_harvesters_geonode:

=================
GeoNode harvester
=================

Introduction
------------

GeoNode provides a CSW endpoint, so it could be harvested using the core CSW harvester.
Anyway using that harvester there is no a clear way to define the different entry types that 
GeoNode provides (layers, maps, documents),
neither it would be possible to retrieve the associated C-READ categories.

A new harvester has been developed from scratch, which harvests from a GeoNode entrypoint, 
using the GeoNode's own APIs.

The extension repository is at http://github.com/geosolutions-it/ckanext-geonode

Installing the GeoNode harvester plugin
---------------------------------------

Before using the plugin, the extension must be installed into the CKAN virtual environment.

As user ``ckan``::

   $ . /usr/lib/ckan/default/bin/activate
   (default)$ cd /usr/lib/ckan/default/src
   (default)$ git clone https://github.com/geosolutions-it/ckanext-geonode.git
   (default)$ cd ckanext-geonode
   (default)$ python setup.py develop

Once done, you have to add to CKAN the plugin ``geonode_harvester`` that the extension provides.

To enable it, edit file ``/etc/ckan/default/production.ini`` and add the plugin::  

   ckan.plugins = [...] geonode_harvester
      
Then restart CKAN to make it load this new extension.  


.. _install_ext_harvesters_ccccc:

=============================
CCCCC ClearingHouse harvester
=============================

Introduction
------------

The CKAN hub have to contain and make searchable also some data already indexed by the CCCCC ClearingHouse.
In order to do this, such data have to be retrieved and stored inside CKAN.

The CCCCC ClearingHouse harvester has been developed from scratch; 
it will query the ClearingHouse and import the metadata, and, when possible,
the related data as well. 
The harvester can also be configured to set the proper CREAD category for each imported record.    
 
The extension repository is at http://github.com/geosolutions-it/ckanext-harvest-clearinghouse

Installing the ClearingHouse harvester plugin
---------------------------------------------

Before using the plugin, the extension must be installed into the CKAN virtual environment.

As user ``ckan``::

   $ . /usr/lib/ckan/default/bin/activate
   (default)$ cd /usr/lib/ckan/default/src
   (default)$ git clone https://github.com/geosolutions-it/ckanext-harvest-clearinghouse.git
   (default)$ cd ckanext-harvest-clearinghouse
   (default)$ python setup.py develop

Once done, you have to add to CKAN the plugin ``clearinghouse_harvester`` that the extension provides.

To enable it, edit file ``/etc/ckan/default/production.ini`` and add the plugin::  

   ckan.plugins = [...] ckanext-harvest-clearinghouse
      
Then restart CKAN to make it load this new extension.  


.. _install_ext_harvesters_geonetwork:

====================
GeoNetwork harvester
====================

Introduction
------------

GeoNetwork is an opensource metadata catalog which provides `CSW <http://www.opengeospatial.org/standards/cat>`_ services.
It was used in older GeoNode versions as the backend for receiving CSW requests.

GeoNetwork may be queried and harvested using the official CSW harvester provides with the 
`ckanext-spatial <https://github.com/ckan/ckanext-spatial>`_ extension, anyway some more functionalities can be 
added using the Geonetwork own API, such as mapping GeoNetwork categories onto CKAN groups.

The `GeoNetwork harvester <https://github.com/geosolutions-it/ckanext-geonetwork>`_ provides such extended functionalities.


Installing the GeoNetowrk harvester plugin
------------------------------------------

Before using the plugin, the extension must be installed into the CKAN virtual environment.

As user ``ckan``::

   $ . /usr/lib/ckan/default/bin/activate
   (default)$ cd /usr/lib/ckan/default/src
   (default)$ git clone https://github.com/geosolutions-it/ckanext-geonetwork.git
   (default)$ cd ckanext-geonetwork
   (default)$ python setup.py develop

Once done, you have to add to CKAN the plugin ``geonetwork_harvester`` that the extension provides.

To enable it, edit file ``/etc/ckan/default/production.ini`` and add the plugin::  

   ckan.plugins = [...] geonetwork-clearinghouse
      
Then restart CKAN to make it load this new extension.  


