Tags: #utilities #netcdf #scientific-computing 

`ncdump` and `ncinfo` are useful introspection tools as part of the [[netCDF Operators (NCO) Tool Suite|NCO suite]].

# Show Dimensions and Variables
## ncdump
`ncdump`'s show header (`-h`) enumerates the dimensions and variables present in a file:
```shell
$ ncdump -h file.nc
netcdf file {
dimensions:
        x = 256 ;
        y = 384 ;
        z = 323 ;
variables:
        float u(z, y, x) ;
        float v(z, y, x) ;
        float w(z, y, x) ;
        float x(x) ;
                x:units = "m" ;
        float y(y) ;
                y:units = "m" ;
        float z(z) ;
                z:units = "m" ;

// global attributes:
                :Cycle = 1 ;
                :dt = 0. ;
}
```
## ncinfo
`ncinfo` summaries the contents of a file more compactly than [[#ncdump|`ncdump` does]]:
```shell
<class 'netCDF4._netCDF4.Dataset'>
root group (NETCDF4 data model, file format HDF5):
    dt: 0.0
    dimensions(sizes): x(256), y(384), z(323)
    variables(dimensions): float32 divh(z, y, x), float32 p(z, y, x), float32 x(x), float32 y(y), float32 z(z), float32 morlet+-50(z, y, x)
    groups:
```

# Show Chunk Sizes
`ncdump` can show special virtual attributes for each variable with `-s`.  This is most useful when [[#Show Dimensions and Variables#ncdump|listing variables]] as the contents of a given variable are usually large an uninteresting in the terminal.

```shell
$ ncdump -sh file.nc
netcdf file {
dimensions:
        x = 256 ;
        y = 384 ;
        z = 323 ;
variables:
        float u(z, y, x) ;
                u:_Storage = "chunked" ;
                u:_ChunkSizes = 1, 384, 256 ;
                u:_DeflateLevel = 2 ;
                u:_Shuffle = "true" ;
                u:_Endianness = "little" ;
        float v(z, y, x) ;
                v:_Storage = "chunked" ;
                v:_ChunkSizes = 1, 384, 256 ;
                v:_DeflateLevel = 2 ;
                v:_Shuffle = "true" ;
                v:_Endianness = "little" ;
        float w(z, y, x) ;
                w:_Storage = "chunked" ;
                w:_ChunkSizes = 1, 384, 256 ;
                w:_DeflateLevel = 2 ;
                w:_Shuffle = "true" ;
                w:_Endianness = "little" ;
        float x(x) ;
                x:units = "m" ;
                x:_Storage = "chunked" ;
                x:_ChunkSizes = 256 ;
                x:_DeflateLevel = 2 ;
                x:_Shuffle = "true" ;
                x:_Endianness = "little" ;
        float y(y) ;
                y:units = "m" ;
                y:_Storage = "chunked" ;
                y:_ChunkSizes = 384 ;
                y:_DeflateLevel = 2 ;
                y:_Shuffle = "true" ;
                y:_Endianness = "little" ;
        float z(z) ;
                z:units = "m" ;
                z:_Storage = "chunked" ;
                z:_ChunkSizes = 323 ;
                z:_DeflateLevel = 2 ;
                z:_Shuffle = "true" ;
                z:_Endianness = "little" ;

// global attributes:
                :Cycle = 1 ;
                :dt = 0. ;
}
```

# 