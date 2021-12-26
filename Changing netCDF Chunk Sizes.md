Tags: #scientific-computing #netcdf

Changing the chunk size requires an out-of-place copy and can be done with NCO's `nccopy`.

The new chunk dimensions are specified as comma separated list of dimensions and their sizes (e.g. `z/1,y/384,x/256` to specify `1x384x256` slices).

```shell
$ nccopy -c z/1,y/384,x/256 /data/iwp/data/R5F04/plot_deflated.${INDEX}.nc /data/iwp/data/R5F04-modified/plot_deflated.${INDEX}.nc
```

Only a subset of variables can be copied and re-chunked using the `-V <variable>[,<variable>...]` option:

```shell
$ nccopy -c z/1,y/384,x/256 -V divh,p /data/iwp/data/R5F04/plot_deflated.${INDEX}.nc /data/iwp/data/R5F04-modified/plot_deflated.${INDEX}.nc
```
