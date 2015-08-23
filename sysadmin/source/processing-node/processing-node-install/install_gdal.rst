
############
Install GDAL
############

We' re going to use `GDAL <http://gdal.org/>`_ to process geospatial data. 

To install it, first add the EPEL 7.5 repository::

    wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
    rpm -ivh epel-release-7-5.noarch.rpm
    yum clean all
    yum check-update

Then install GDAL::

    yum install gdal

And GDAL's python bindings::

    yum install numpy scipy python-matplotlib ipython python-pandas sympy python-nose
