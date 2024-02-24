Tags: #fortran 

Even though newer versions of Fortran will allocate an `allocatable` variable when it is assigned a value, this does not carry over to internal files.  When writing to an `allocatable` character array, it must be allocated before use - either by specifying a maximum array length or computing the required length on the fly.

The following Fortran is not valid and likely will result in an inscrutable error message at run-time:
```fortran
character(len=:), allocatable :: some_string
character(len=:), allocatable :: internal_file

some_string = "hello"

write( internal_file, "(A,A)" ) some_string, " world"
```

GNU gfortran with debugging turned on will generate a run-time error indicating `Fortran runtime error: End of record`.


