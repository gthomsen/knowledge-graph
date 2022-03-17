Tags: #software-engineering #fortran 

# Free Format Source
Source lines do not have constraints on which columns can be used.  Individual lines can be up to 132 characters long.

# Dynamic Memory Management
Introduced `allocatable` arrays that are allocated/deallocated via `allocate()` and `deallocate()`, respectively.

Allocated memory must be deallocated when no longer used, otherwise a memory leak will occur.  Fortran95 introduced [[Fortran95 Features#Automatic Deallocation|automatic deallocation]] when an `allocatable` object went out of scope.

# User-defined Data Types
User-defined data types can be specified via the `type` directive:
```fortran
type shape
    real    :: x
    real    :: y
    integer :: shape_type
end type shape
```

Individual components (`x`, `y`, and `shape_type` above) cannot be allocatable.  Allocatable components were introduced in Fortran 2003.