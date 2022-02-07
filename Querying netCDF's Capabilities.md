Tags: #netcdf #utilities 

Each netCDF installation provides `nc-config` as a means for querying its capabilities and reporting flags for compiling/linking against it.

```shell
$ nc-config --all

This netCDF 4.7.3 has been built with the following features:

  --cc            -> /usr/bin/cc
  --cflags        -> -I/usr/include -I/usr/include/hdf5/serial
  --libs          -> -L/usr/lib/x86_64-linux-gnu -L/usr/lib/x86_64-linux-gnu/hdf5/serial -lnetcdf
  --static        -> -lhdf5_hl -lhdf5 -lpthread -lsz -lz -ldl -lm -lcurl
...
```

Individual components can be queried as well:
```shell
$ nc-config --fflags
-I/usr/include
$ nc-config --flibs
-L/usr/lib/x86_64-linux-gnu -lnetcdff -Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-z,now -lnetcdf -lnetcdf -ldl -lm
```

# Determining Parallel Support
Parallel netCDF I/O requires a lot of things to be setup, including:
- Parallel HDF5 support compiled in
- Parallel netCDF support compiled in
- Parallel netCDF access requested

The following indicates whether a particular netCDF installation has parallel capabilities:
```shell
$ nc-config --has-parallel --has-pnetcdf
no
no
```