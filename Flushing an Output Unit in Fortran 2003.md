Tags: #fortran #scientific-computing

Fortran 2003 provides a `flush()` statement which makes data on a particular output unit available to other processes (or available via a `read()` statement).  This supersedes vendor-specific `flush()` intrinsics that existed prior to inclusion in the standard.

Things of note:
- `flush()` requires a unit and there is no standard for flushing all units. 
- The `*`  default output unit is available via the `iso_fortran_env::OUTPUT_UNIT` variable.

```fortran
    use, intrinsic iso_fortran_env, only:    OUTPUT_UNIT
    
    write( *, * ) "Hello, world!"

    flush( OUTPUT_UNIT )
```