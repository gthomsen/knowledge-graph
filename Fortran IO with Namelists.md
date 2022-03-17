Tags: #software-engineering #scientific-computing #fortran 

Namelists are a legacy method to specify key-value configuration text files.  

Defining them in the code is done like so:
```fortran
    NAMELIST /config_values/ &
        key1, &
        key2, &
        ...
        keyN
```

And are read and written with the `nml` parameter in lieu of the `fmt` parameter:
```fortran
read( io_unit,  nml=config_values )
write( io_unit, nml=config_values )
```

The above parses and writes the following file (the case can differ, see the [[#Namelist Requirements|requirements]] below):
```
&config_values
key1 = value1
key2 = value2
...
keyn = value
/
```

# Namelist Requirements
Formatting requirements of a namelist file (see Modern Fortran Explained section 9.10):
1. The namelist declaration must not contain whitespace between the ampersand and the namelist name.  `&config_values` is valid, but `& config_values` is not.
2. Whitespace may precede the namelist declaration.
3. The trailing slash (`/`) is required.
4. Order of key/value pairs does not have to match the definition.
5. Case does not matter for the keys in the namelist file.
6. Whitespace may precede or follow keys in the namelist file.
7. Comments may appear at the end of the line, or on their own line may, be specified by `!`.

## Reading
The order of keys in the file does not have to match the namelist's definition.  Variables corresponding to a missing key are not modified during the `read()` and retain their previous value.

Case for the keys does not matter and is ignored.

Whitespace before and after the `=` separator is ignored.

Keys may be repeated multiple times and the value is that of the last encountered key.

## Writing
The namelist name and all keys are written in upper-case.

## Portability
Some compilers are lenient when parsing a namelist file which leads to portability issues between systems.  Just because one compiler reads a namelist file does not mean that it correct.

Debugging a non-compliant namelist file can be a pain, and may manifest in a number of ways (e.g. [[End of File in Fortran IO|EOF encountered]] and nothing more).

Check the following when I/O errors occur:

- [No spaces between start of name list and its name](https://stackoverflow.com/questions/35758473/error-using-namelist-in-gfortran)
- Make sure line endings are consistent and match the OS
- Move the trailing slash to a new line