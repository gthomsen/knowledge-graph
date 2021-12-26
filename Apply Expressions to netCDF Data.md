Tags: #scientific-computing #netcdf 

[[netCDF Operators (NCO) Tool Suite|NCO]]'s `ncap2` allows application of algebraic expressions to netCDF file's variables.  This is useful to avoid writing custom code to open, read, compute, and write data when the expressions are simple.

Dividing the `x`, `y`, and `z` variables by `0.15`:
```shell
$ ncap2 -s 'x=x/0.15;y=y/0.15;z=z/0.15;' in.nc out.nc
```

# Changing Chunk Size
Chunk sizes can be modified while applying expressions via the `--cnk_dmn=DIM/SIZE` to avoid an extra copy just to [[Changing netCDF Chunk Sizes|modify the chunk size]]:
```shell
# change the dimensions to 1x384x256 XY slices.
$ ncap2 --cnk_dmn=z,1 --cnk_dmn=y,384 --cnk_dmn=x,256 -s 'value=u*10.0;' in.nc out.nc
```

# Precision
One needs to be careful about apply expressions to floating point data so as to avoid unwanted promotion of data types.  The expression `x=x/1.0` will result in a `float32` being promoted to `float64`, while `x=float(x/1.0)` will keep it as `float32`.