Tags: #software-engineering #fortran #scientific-computing 

Collection of Fortran snippets that are actually undefined behaviors.

# Limited Operations on Unallocated Arrays
None of the shape or size methods can be called on unallocated arrays.

```fortran
integer, allocatable :: int_array(:)
integer              :: number_dimensions(:)
integer              :: number_entries

! undefined!
number_entries    = size( int_array )
number_dimensions = shape( int_array )
```

Additionally, the `lbound()` and `ubound()` methods, for lower- and upper bounds respectively, are undefined as well.

See "Modern Fortran Explained" section 8.12.2 or this [Stack Overflow post](https://stackoverflow.com/questions/31373727/size-of-array-after-a-deallocate) for additional details.

# Conditionals Do Not Short Circuit
Unlike C and C++, Fortran does not define the evaluation order of conditionals so short circuiting evaluation does not occur.  This is particularly problematic when working with optional arguments.  The following is broken:

```fortran
if present( optional_argument ) .and. (optional_argument > 1) then
    ! do something based on optional_argument.
endif
```

If `optional_argument` is not present, then evaluating the conditional results in undefined behavior.  Some compilers will happily skip the above, while others will result in a invalid memory access (i.e. segmentation fault).

# intent(out) Dummy Arguments
Upon entry into a procedure any arguments that have the `intent(out)` attribute specified are considered undefined upon entry (with the exception of type components with [[Fortran 2003 Features#Component Default Initialization|default initialization]]).

 `allocatable` arguments are a special case where an allocated host variable supplied as an `intent(out)` dummy variable will be deallocated upon entry into the routine.  Thus, the following is undefined:
 ```fortran
 ! NOTE: this is a contrived interface to demonstrate the phenomena.
 subroutine invalid_initialize_result( allocated_size, default_value, real_array )
     integer, intent(in)            :: allocated_size
     real, intent(in)               :: default_value
     real, allocatable, intent(out) :: real_array(:)

     ! real_array is deallocated upon entry into the method!
     real_array(1:allocated_size) = default_value
end subroutine invalid_initialize_result
```

 