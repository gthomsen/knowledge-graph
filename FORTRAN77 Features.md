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