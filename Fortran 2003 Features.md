Tags: #software-engineering #fortran 

# Array Initialization
Prior to Fortran 2003, [[Fortran Features#Array Initialization|arrays were initialized]] with a list delimited by slashes (`/`):
```fortran
real :: x(5) = / 1.0, 2.0, 3.0, 4.0, 5.0 /
```

Where as Fortran 2003 allows square brackets:
```fortran
real :: x(5) = [ 1.0, 2.0, 3.0, 4.0, 5.0 ]
```

# Command Line Parsing
`get_command_argument()` and `command_argument_count()` were introduced to standardize command line parsing.  

Handling arbitrary length command line arguments should be done with the following pattern:
1. Verify you have the ith argument using `command_argument_count()`
2. Query the length of the ith argument using `get_command_argument( i, length=argument_length )`
3. Allocate space according to the queried length
4. Retrieve the command line argument using `get_command_argument( i, value=argument_value )`

See here for [[Command Line Parsing in Fortran|details on deferred length arrays and command line parsing]].

# Procedure Pointers
Just like pointers can point to data, procedure pointers can point to procedures.  There are limitations on which procedures can be pointed too (presumably limited to non-type methods), though this limitation may be addressed in [[Fortran 2008 Features#Procedure Pointers Can Point to Internal Methods|Fortran 2008]].

## The pass Attribute
`pass` specifies whether an additional argument is passed to the procedure pointed to.  When used with derived type methods, this governs whether the calling object is supplied or not (i.e. the `this` pointer in C++).

Specifying `pass( ARGUMENT )` indicates that the type instance should be supplied as `ARGUMENT` rather than the first argument to the method.

See this [PGI blog post](https://www.pgroup.com/blogs/posts/f03-oop-part1.htm) for use of `pass`.  This [Stack Overflow post](https://stackoverflow.com/a/25413107) indicates that `pass` is default, though explicitly specifying it makes that obvious.

Care needs to be taken since some earlier versions of OpenMP (v4.0 and older) do not properly handle `pass`.  See [here for a confirmation](https://community.intel.com/t5/Intel-Fortran-Compiler/Is-OpenMP-not-supporting-Fortran-2003-PASS-Finalization-etc/m-p/1034161) by [[Who's Who In Fortran#Steve Lionel|Steve Lionel]].

# Derived Types
## Type-Bound Procedures
A type's procedures are called type-bound procedures and are declared inside of the `type` definition, but only after the `contains` keyword.
## Overriding Methods
When types are extended, they may either:
1. Augment the interface by adding new methods
2. Reimplement the interface by replacing existing methods

For #2, the derived type overriding its ancestor's implementation, it must specify that a method is overriding via the `module subroutine` / `module function` statement instead of the normal `subroutine` / `function` statements.

### Preventing Override
There are times where the base type's methods should **not** be reimplemented, and derived types are prevented from doing so when a method has the `non_overridable` attribute.  This makes sense when the base type's methods are integral for its (and any derived types') functionality.

For example, an abstract grid class may require that the accessors to its domain and length are always implemented by itself, rather than a derived type:

```fortran
type, abstract :: grid
    real    :: domain(2)
    integer :: number_grid_points
    ...

contains
    ! the domain() and length() methods will always use the grid type's
    ! implementation, regardless of additional type derivations.
    procedure, pass, non_overridable :: domain => grid_domain
    procedure, pass, non_overridable :: length => grid_domain_length
    ...
end type
```

## Abstract Types
Intended to be derived from and have their interface implemented.

The `abstract` attribute goes on the type declaration, and the `deferred` attribute goes on procedures that abstract.

### Deferred Bindings
Abstract types can define abstract methods that must be overridden by derived types (`virtual` functions in C++ parlance).  This is done like so:

```fortran
type, abstract :: list
    ...
    contains
        ! abstract method is print_list() and all derivations must follow
        ! the interface defined by print_values().
        procedure(print_values), deferred :: print_list
end type list

abstract interface

subroutine print_values( this )
    import list
    class(list) :: this

    ! no definition goes here since it will be provided by a derived type.
end subroutine

end interface
```

# Allocations and Reallocations
## Reallocations
Objects on the left-hand side can be reallocated during assignment if the shape of right-hand side differs.  In Fortran 95 the following code was illegal:

```fortran
real, allocatable :: a(:), b(:), c(:)

allocate( a(10) )
allocate( b(20) )

a = 1
b = 2

! assignment allocates c with 10 elements.
c = a

! assignment reallocates c with 20 elements.  this was previously illegal
! in Fortran 95.
c = b
```

## Transferring Allocations
Unsurprising given its name, `move_alloc()` transfers an allocatable object to another. 