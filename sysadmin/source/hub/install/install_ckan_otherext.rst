.. _install_ckan_other:

#####################
Other CKAN extensions
#####################

============
Introduction
============

In this document you'll only find specific information for installing some CKAN official and 
unofficial extensions.

.. _extension_tracker:

=======
Tracker
=======

Tracks visit to the site and to single datasets.

.. hint::
   Doc page at http://docs.ckan.org/en/tracking-fixes/tracking.html
    
Edit the file ``/etc/ckan/default/production.ini`` and add the line ::

   ckan.tracking_enabled = true
   
Then create a script ``tracker_update.sh`` like this::

    #!/bin/bash

    . /usr/lib/ckan/default/bin/activate

    paster --plugin=ckan tracking update         -c /etc/ckan/default/production.ini 
    paster --plugin=ckan search-index rebuild -r -c /etc/ckan/default/production.ini

You can use this file directly to run the index rebuilding, or use it in cron to make it run periodically.

As user ``root`` use ::

     crontab -e -u ckan
     
or as user ``ckan``::

     crontab -e
     
and add the line::

   0 * * * * /usr/lib/ckan/tracker_update.sh >>/var/log/ckan/tracker.log 2>&1


======================
Multilingual extension
======================

.. hint::
   Info page at http://docs.ckan.org/en/latest/maintaining/multilingual.html

The Multilingual extension is aleady checked out together with the main CKAN repository,
so its sources are already available on the system.

In order to enable the multilingual plugin, you have to edit the file 
``/etc/ckan/default/production.ini`` and add the `multilingual` plugins::

   ckan.plugins = [...] multilingual_dataset multilingual_group multilingual_tag
   
and restart CKAN in order to reload the plugin list::

   service supervisord restart   

Then follow the details in the official page in order to add the translated entries.
 
.. hint::
   Official documentation is not yet complete (as of 2014-02-17).  
   
   See also https://github.com/ckan/ckan/issues/1021
   
The solr schema file ``/etc/solr/ckan/conf/schema.xml`` should be updated with the one with 
multilang capabilities::

   ln -sf /usr/lib/ckan/default/src/ckan/ckanext/multilingual/solr/schema.xml /etc/solr/ckan/conf/schema.xml
   
Then also link all the stopword files::

   for txtfile in /usr/lib/ckan/default/src/ckan/ckanext/multilingual/solr/*.txt ; do ln -sv $txtfile /etc/solr/ckan/conf/  ; done

Restart solr::

   service solr restart   
      
You have to rebuild the index with the new schema.
As ``ckan`` user, ``activate`` the virtual env and run::

   paster --plugin=ckan search-index rebuild --config=/etc/ckan/default/production.ini
   
    
.. warning::
   It causes lots of *CRITICAL* logging due to old code::
    
      CRITI [ckan.logic] Action `term_translation_show` is being called directly all action calls should be accessed via logic.get_action
      
   The fix https://github.com/ckan/ckan/issues/1520 has been applied.      
      
.. warning::
   Multilingual seems not very stable: it breaks on some situations::
   
      Error - <type 'exceptions.AttributeError'>: 'int' object has no attribute 'get'

   and this will make the client display an "Internal error" message. 
         
   *Not enabled* for now.   

.. warning::
   When replacing the schema file, remember to also add the settings for indexing the spatial fields, 
   as reported in :ref:`configure_spatial_search`.

   
