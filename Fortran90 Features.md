Tags: #software-engineering #fortran 

# Free Format Source
Source lines do not have constraints on which columns can be used.  Individual lines can be up to 132 characters long.

# Dynamic Memory Management
Introduced `allocatable` arrays that are allocated/deallocated via `allocate()` and `deallocate()`, respectively.  Arrays allocated in this manner are called deferred-shape arrays, as the variable's final size/shape is deferred until run-time.

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

# Assumed-Shape Arrays
Assumed-shape arrays have their dimensionality specified by one or more colons (`:`), which allows the compiler to use said arrays in whole-array expressions.

```fortran
subroutine compute_assumed_shape_array( array )

    real, dimension(:) :: array
    
    ! This definition is also equivalent:
    ! real :: array(:)

    write( *, * ), 'Array has shape ', shape( array ), ' and size ', size( array )
end subroutine
```

Replaced [[FORTRAN77 Features#Assumed-Size Arrays|assumed-sized arrays]] as the recommended way to pass arrays into methods as it allows the use of `shape()` and `size()` to query their sizes and avoid out-of-bounds errors.  The extra information available to the compiler to support `shape()` and `size()` allows said arrays to be used in whole-array expressions.