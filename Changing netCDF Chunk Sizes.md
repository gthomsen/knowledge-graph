Tags: #scientific-computing #netcdf

Changing the [[Chunking in netCDF|chunk size]] requires an out-of-place copy and can be done with NCO's `nccopy`.

The new chunk dimensions are specified as comma separated list of dimensions and their sizes (e.g. `z/1,y/384,x/256` to specify `1x384x256` slices).

```shell
$ nccopy -c z/1,y/384,x/256 /path/to/data/dataset.nc /path/to/data/new-dataset.nc
```

Only a subset of variables can be copied and re-chunked using the `-V <variable>[,<variable>...]` option:

```shell
$ nccopy -c z/1,y/384,x/256 -V u,v /path/to/data/dataset.nc /path/to/data/new-dataset.nc
```
