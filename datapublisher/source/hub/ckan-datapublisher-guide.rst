
This user guide covers using C-READ Hub's web interface to find
data. C-READ Hub is based on CKAN wich has a powerful API (machine interface),
which makes it easy to develop extensions and links with other information systems.

--------
Overview
--------

CKAN is a tool for making open data websites. (Think of a content management
system like WordPress - but for data, instead of pages and blog posts.) It
helps you manage and publish collections of data. It is used by national and
local governments, research institutions, and other organizations who collect a
lot of data.

Once your data is published, users can use its faceted search features to
browse and find the data they need, and preview it using maps, graphs and
tables - whether they are developers, journalists, researchers, NGOs, citizens,
or even your own staff.

Datasets and resources
======================

For CKAN purposes, data is published in units called "datasets". A dataset is a
parcel of data - for example, it could be the crime statistics for a region,
the spending figures for a government department, or temperature readings from
various weather stations. When users search for data, the search results they
see will be individual datasets.

A dataset contains two things:

* Information or "metadata" about the data. For example, the title and
  publisher, date, what formats it is available in, what license it is released
  under, etc.

* A number of "resources", which hold the data itself. CKAN does not mind what
  format the data is in. A resource can be a CSV or Excel spreadsheet, XML file,
  PDF document, image file, linked data in RDF format, etc. CKAN can store the
  resource internally, or store it simply as a link, the resource itself being
  elsewhere on the web. A dataset can contain any number of resources. For
  example, different resources might contain the data for different years, or
  they might contain the same data in different formats.


-------------------
Usage Documentation
-------------------



.. _finding_data:

Finding data
============

Searching the site
------------------

To find datasets in CKAN, type any combination of search words (e.g. "health",
"transport", etc) in the search box on any page. CKAN displays the first page
of results for your search. You can:

* View more pages of results

* Repeat the search, altering some terms

* Restrict the search to datasets with particular tags, data formats, etc using
  the filters in the left-hand column

If there are a large number of results, the filters can be very helpful, since
you can combine filters, selectively adding and removing them, and modify and
repeat the search with existing filters still in place.

If datasets are tagged by geographical area, it is also possible to run CKAN
with an extension which allows searching and filtering of datasets by selecting
an area on a map.

.. image:: /images/search_the_site.jpg


Searching within an organization
--------------------------------

If you want to look for data owned by a particular organization, you can search
within that organization from its home page in CKAN.

#. Select the "Organizations" link at the top of any page.

#. Select the organization you are interested in. CKAN will display your
   organization's home page.

#. Type your search query in the main search box on the page.

CKAN will return search results as normal, but restricted to datasets from the
organization.


Exploring datasets
------------------

When you have found a dataset you are interested and selected it, CKAN will
display the dataset page. This includes

* The name, description, and other information about the dataset

* Links to and brief descriptions of each of the resources

.. image:: /images/exploring_datasets.jpg

The resource descriptions link to a dedicated page for each resource. This
resource page includes information about the resource, and enables it to be
downloaded. Many types of resource can also be previewed directly on the
resource page. .CSV and .XLS spreadsheets are previewed in a grid view, with
map and graph views also available if the data is suitable. The resource page
will also preview resources if they are common image types, PDF, or HTML.

The dataset page also has two other tabs:

* *Activity stream* -- see the history of recent changes to the dataset

* *Related items* -- see any links to web pages related to this dataset, or add
  your own links.

