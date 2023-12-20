Tags: #software-engineering #fortran 

# Automatic Deallocation
Allocated objects are implicitly `deallocate()`'d when they go out of scope.  In Fortran90, this would result in a memory leak.

## Allocatable Dummy Arguments
One exception to the automatic deallocation change are `allocatable` dummy arguments.  If a dummy argument is allocated within a subroutine or function, the caller is responsible for explicitly deallocating the variable.

Consider the following:
```fortran
program allocation_test
    integer           :: array_length = 1024
    real, allocatable :: array(:)

    call allocate_array( array_length, array )

    ! NOTE: this is required as array will not be deallocated at the end of
    !       this block.
    deallocate( array )

end program allocation_test

subroutine allocate_array( array_length, array )
    integer, intent(in)            :: array_length
    real, allocatable, intent(out) :: array

    allocate( array(array_length) )

    ! array is not automatically deallocated since it is an allocatable
    ! dummy argument.  the caller is responsible for calling deallocate().
    
end subroutine allocate_array
```

# Pure and Elemental Procedures
User-defined `pure` and `elemental` procedures can be defined.

# Component Initialization
Default initialization rules for user-defined type were specified.

# Modules
Code can be organized and reused through modules.  Provides a scope to a subset of global variables.  Calling code can incorporate a module's variables wholesale (`use module`) or as needed (`use module, only: var1, var2`).

By default, module variables do not retain their values and require explicit annotation with the `save` attribute.  [[Fortran 2008 Features#Module Variables are Saved|All variables implicitly have the `save` attribute]] in Fortran 2008.

# Minimal Width Formatting
The `I0` edit descriptor was introduced so that integers could be written without knowing how many digits were needed, or with additional padding.