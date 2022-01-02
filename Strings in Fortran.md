Tags: #fortran #scientific-computing

Processing strings in Fortran is unpleasant at best.  The table below names different arrangements of characters (that are often confused as strings) so they can be searched for or litigated by a language lawyer.

| Name | Example |
| --- | --- |
| Array of characters | `character, dimension(80) :: array_of_chars` |
| Scalar string | `character(len=80) :: scalar_chars` |
| Array of strings | `character(len=80), dimension(60) :: string_array`|

Arrays of strings are index like so:
```fortran
string_array(string_index)(1:substring_index) = 'A'
```

# Deferred Length Allocations
Scalar strings that are allocatable are called Deferred Length Allocations.  These are used when the string length is unknown until run-time, typically used to parse newer, variable length configuration files.  Their declarations look like so:

```fortran
characeter(len=:), allocatable, dimension(:) :: strings
```

For posterity, and the unfortunate souls who work on ancient systems, gfortran [did not support Deferred Length Allocations properly until v5.2.0](https://gcc.gnu.org/bugzilla/show_bug.cgi?id=54070).  And by did not support, I mean, crashed with an internal compiler error.