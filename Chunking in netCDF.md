Tags: #netcdf #scientific-computing #performance

On disk, netCDF variables are broken up into chunks which are the granularity at which the variable is interacted with.  

Unicar's documentation on [why chunking impacts performance](https://www.unidata.ucar.edu/blogs/developer/entry/chunking_data_why_it_matters) and [how to choose chunk shapes](https://www.unidata.ucar.edu/blogs/developer/en/entry/chunking_data_choosing_shapes).