.. _install_ext_cread:

####################################
Installing C-READ extension for CKAN
####################################

============
Introduction
============

The C-READ extension provides customization for:

- general styling
- main page layout
- display of items in the dataset list
- display of item in dataset page
- categories filtering


.. hint::
   Ref info page at https://github.com/geosolutions-it/ckanext-cread


In this document you'll only find specific information for installing the CREAD plugin for CKAN. 

It is expected that CKAN has already been properly installed and configured as described 
in :ref:`install_ckan`.


.. _extension_cread:

================
C-READ extension
================

In order to install the ckanext-cread, copy (or clone using git) the ``ckanext-cread/`` directory inside 
the CKAN src directory (i.e. ``ckan/default/src``).

Before using the plugin, the extension must be installed into the CKAN virtual environment.

As user ``ckan``::

   $ . /usr/lib/ckan/default/bin/activate
   (default)$ cd /usr/lib/ckan/default/src
   (default)$ git clone https://github.com/geosolutions-it/ckanext-cread.git
   (default)$ cd ckanext-cread
   (default)$ python setup.py develop

Once done, you can add the plugin ``cread_theme`` that the CREAD extension provides.

To enable it, edit file ``/etc/ckan/default/production.ini`` and add the plugin::  

   ckan.plugins = [...] cread_theme
   
   
Restart CKAN to make it load this new extension.  
