Tags: #netcdf #utilities #scientific-computing #unfinished 

netCDF supports [compression](https://www.unidata.ucar.edu/blogs/developer/entry/netcdf_compression) though it has two parameters for controlling performance including the compression level and whether the data are shuffled prior to compression.  `nccopy` 

Deflation and shuffle configuration can be queried via [[netCDF File Inspection Tools#Show Chunk Sizes| `ncdump -sh`]].

The amount of compression applied is an integer between 1 and 9, with 1 being the fastest and 9 being the smallest.  Specifying 0 disables compression.  Note that higher levels of compression result in a non-trivial amount of CPU utilization during read/write.

# Changing Deflation Parameters During File Copy
Changes to a variables deflation level cannot be made once the variable is written to file.  Coupled with netCDF's design decision to disallow removal of a variable from a file, this means changing deflation parameters can only be done when writing a new file. `nccopy` supports this.

```shell
$ nccopy -d 2 -s input.nc output.nc
```

Changing [[Changing netCDF Chunk Sizes|chunk sizes and copying a subset of available variables]] can be done while changing deflation parameters.