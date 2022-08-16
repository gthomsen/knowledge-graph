Tags: #fortran #mpi

Fortran 2003 and 2008 provide typed interfaces to the MPI API.  The Fortran 2003 interface is available via `use mpi` while the Fortran 2008 interface is available via `use mpi_f08`.  They are both improvements over the legacy `include mpif.h`, while the Fortran 2008 interface improves the types, shape/rank/etc characteristics, and intents of dummy arguments making it more useful for catching issues at compile time.

# Differences
Communicators are no longer `INTEGER` but rather `TYPE(MPI_Comm)`.  The error below is self explanatory, though somewhat surprising when moving from `use mpi` to `use mpi_f08`:
```
PartInit.f90(33): error #6633: The type of the actual argument differs from the type of the dummy argument.   [TRACK_WORLD]
    call MPI_COMM_SIZE( TRACK_WORLD, noOfProcessors, ierr )
------------------------^
```

Note that this can also crop up when the build system does not manage its dependencies properly and has a stale module file (`foo.mod`) that provides the old interface that conflicts against the current code.