.. _cread-arch-data:

Data node
=========

The data node is the core of the whole system. 
It contains all the data and related metadata of the CREAD system, and provides OGC services to retrieve the data using standard
protocols.

This node is implemented by GeoNode and GeoServer. 

GeoNode provides some user friendly functionalities around GeoServer features, 
serving also as a local catalog and allowing users to upload non geographic data.

GeoServer is the real "geographic engine" behind GeoNode, offering a wide set of OGC services.
  