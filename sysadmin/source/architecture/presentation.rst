.. _cread-arch-presentation:

Presentation node (hub)
=======================

The hub gathers all the metadata distributed in the various C-READ nodes and present them to 
the user as a single catalog view. The hub offers the user a front end toward the catalog and the geographic data. 

It is implemented by CKAN, a data portal for the the storage and distribution of data.

Note that this is the only node that external users (or better, users which are only data consumers) need to access to.


This node is only an aggregation node: no data will ever be uploaded by users on this node. 
All of the presented data and metadata are harvested from other nodes.

The main node that is harvested is of course the CREAD data node, but other sites can be harvested as well, provided they expose
an entrypoint using a known protocol.

For instance, CSW nodes can be harvested using the CSW harvester provided by the official spatial extension.
Harvesters for other sites can be developed from scratch: for instance an harvester for the CCCCC Clearinghouse has been developed
within the DMS project.       
