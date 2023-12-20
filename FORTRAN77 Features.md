Tags: #fortran 

Miscellaneous facts about Fortran that cannot be otherwise attributed to a newer standard. 

# Types of Arrays
## Explicit-shape Arrays
Explicit-shape arrays have their size explicitly specified by a constant, or a `parameter`, resulting in constant bounds known at compile-time: 
```fortran
subroutine compute_explicit_shape_array( )

    integer, parameter :: array_length = 100
    
    real               :: array1(array_length)  ! explicit-shape array of size 100.
    real               :: array2(10)            ! explicit-shape array of size 10.
    ...
end subroutine    
```

## Automatic Arrays
Automatic arrays have their size provided as a dummy argument and are typically allocated on the stack ([[Fortran Compiler Support#Controlling Stack Allocations|unless specified by a compiler flag]]):
```fortran
subroutine compute_automatic_array( array_length )

    integer, intent(in) :: array_length
    
    real                :: array3(array_length)  ! automatic array whose size is typically known
                                                 ! at run-time.
    ...
end subroutine    
```

Some compilers allow command line options to specify the location of automatic arrays (e.g. [[Fortran Compiler Support#Controlling Stack Allocations|ifort's `-heap-arrays`]]).

## Assumed-Size Arrays
Assumed-size arrays do not have any shape information present, which limits their use as they cannot be a result from a function, have a polymorphic type (in Fortran 2003 and newer), etc.  
```fortran
subroutine compute_assumed_size_array( array )

    real :: array(*)

    ! This definition is also equivalent:
    ! real :: array(*)

end subroutine
```

***NOTE:*** This is considered a legacy feature and should be avoided in favor of [[Fortran90 Features#Assumed-Shape Arrays|assumed-shape arrays]] found in [[Fortran90 Features|Fortran90]].

## Formatted I/O
### Internal Files
Data can be converted to/from a string using a character variable as an internal file.  This is done via the `write()` and `read()` routines with a character variable provided as the I/O unit:

```fortran
character(len=128) :: formatted_message

! formatted_message == "Hello, world - 123456"
write( formatted_message, "(A, I0)" ) "Hello, world - ", 123456
```

***NOTE:*** At least through [[Fortran 2003 Features|Fortran 2003]] (possibly [[Fortran 2008 Features|Fortran 2008]], the specified character variable must be allocated or associated prior to the call to `write()` or `read()`.  See [this Intel Forums post](https://community.intel.com/t5/Intel-Fortran-Compiler/internal-formatted-write-to-deferred-length-allocatable/td-p/751843) where the Fortran 2008 standard's language is discussed.

### Conditional Termination Specifier
The colon (`:`) edit descriptor allows a format specifier to be conditional and provides formatting control if the I/O list has not been exhausted.  If it has been exhausted, it is skipped.  

This uncommon specifier allows for comma-delimited output like so:
```fortran
integer :: integer_array(3)

integer_array(1) = 10
integer_array(2) = -1
integer_array(3) = 55

! Prints "Integer array: 10-155"
write( *, '(A,*(I0))' ) "Integer array: ", integer_array

! Prints "Integer array: 10, -1, 55"
write( *, '(A,*(I0:", "))' ) "Integer array: ", integer_array
```