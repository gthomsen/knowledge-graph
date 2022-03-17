Tags: #software-engineering #fortran #scientific-computing 

Derived types were introduced in Fortran 2003 and provide an object-oriented program.  To the surprise of those coming from C++, allocation is separate from initialization and, therefore, constructors don't exist. 

Allocation is performed via `allocate()` and the object's components are uninitialized.  

Therefore, the contents of an object of type `thing` (see below) are undefined until they are initialized:
```fortran
type thing
    integer              :: int
    real                 :: float
    integer              :: int_shaped_array(10)
    integer, allocatable :: int_allocatable_array(:)
end type thing
```

Individual components can be initialized at type definition (read: compile time) to a fixed value.  Not all components of a type have to be initialized and those that are not, have undefined values until they're initialized.

```fortran
type thing_with_defaults
    integer              :: int   = 3
    real                 :: float = 3.14159
    integer              :: int_shaped_array(10)      ! undefined contents
    integer, allocatable :: int_allocatable_array(:)  ! unallocated
end type thing
```

In theory, structure initialization can specify different values at run-time with declarations like so:

```fortran
! initialization via assignment (NOTE: this doensn't compile with gfortran 9.3).
type(thing_with_defaults) :: thing_instance = thing_with_defaults( int=9 )
```

Though I cannot 1) find the correct syntax, or 2) confirm it works.

# Allocatable Type Components
As far as I understand, allocatable components can only be initialized at run-time.  Therefore, code needs to [[Undefined Behavior in Fortran#Limited Operations on Unallocated Arrays|guard against access to unallocated arrays]] to maintain defined behavior.
