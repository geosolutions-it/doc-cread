.. _cread-arch-processing:

Processing nodes
================

A processing node creates resources to be published, and sends them to the data node for publishing.

A processing node only runs processing services; it will not run services to disseminate data and 
metadata to the public. Once the product is ready, it will be transferred to the data node  as part of the processing script,
where it will be published. 

There are two different kinds of processing nodes: automated and attended.


Automated processing node
-------------------------

Automated processing nodes are implemented using Jenkins.

Jenkins is a web based tool for running and monitoring the execution of custom scripts.
We'll have jenkins run scripts which extract data from known sources, transform them in data publishable by the CREAD system 
and send the data to the data node.

Script execution can be triggered on a time basis, so 

Only administrators need to access tot he Jenkins site to install new scripts and monitor the processes, 
since processed data can be viewed by the end users on the hub once it's ready.


Attended workflow node
----------------------

Attended processing is implemented by QGIS, a desktop GIS application.
By the use of a simplified interface for running workflows, users can be taught the basics of GIS processing.
The implemented workflows will also enable the user to create new layers in the data node. 

 