Tags: #software-engineering #fortran 

[NAG's summary of changes](https://www.nag.com/nagware/np/r61_doc/nag_f2003.html) introduced in Fortran 2003.  The [ISO specification](https://wg5-fortran.org/f2003.html).

# Array Initialization
Prior to Fortran 2003, [[Fortran Features#Array Initialization|arrays were initialized]] with a list delimited by slashes (`/`):
```fortran
real :: x(5) = / 1.0, 2.0, 3.0, 4.0, 5.0 /
```

Where as Fortran 2003 allows square brackets:
```fortran
real :: x(5) = [ 1.0, 2.0, 3.0, 4.0, 5.0 ]
```

# Allocatable Dummy Arguments
Fortran 95 allowed allocatable objects to be supplied as [[Fortran Features#Actual vs Dummy Arguments|actual arguments]] to procedures, though Fortran 2003 allowed dummy arguments to be allocatable.

Thus, the following code is invalid Fortran 95 but valid Fortran 2003:
```fortran
function allocate_object( number_elements, default_value ) result( real_array )
    integer, intent(in) :: number_elements
    real, intent(in)    :: default_value
    real, allocatable   :: real_array(:)

    allocate( real_array(number_elements) )

    real_array(:) = default_value
end function allocate_object
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
## Allocatable Components
Components in user-defined data types can now be `allocatable`.  [[Fortran90 Features#User-defined Data Types|Previously]], all component characteristics must be known at compile time.

## Component Default Initialization


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

Anatomy of the  `print_list()` declaration:
- `print_list` is the type-bound procedure name
- `print_values` is the interface name
- `import list` defines the `list` type within the `print_values()` interface (there is no host association with interface blocks)
 
# Polymorphism

## type() vs class()
A derived type can be used with both the `type()` and `class()` keywords and is somewhat confusing to those new to OOP in Fortran.

The following code defines a hierarchy of shape types where `shape` is the base type, `rectangle` is a `shape`, and `square` is a `rectangle`:
```fortran
! shapes have a location and a color.
type shape
    integer :: x
    integer :: y
    integer :: color
end type shape

! rectangles are shapes that have a length and a width.
type, extends(shape) :: rectangle
    integer :: length
    integer :: width
end type rectangle

! squares are special rectangles.
type, extends(rectangle) :: square
end type square
```

Use `type()` when defining a concrete object objects:
```fortran
subroutine do_stuff()
    type(rectangle) :: rect1, rect2

    ! print the sum of their lengths.
    write(*,*) rect1%length + rect2%length
    
end subroutine do_stuff
```

Use `class()` when specifying which types are allowed:
```fortran
subroutine do_rectangle_stuff( rect1, rect2 )
    class(rectangle), intent(in) :: rect1, rect2

    ! print the sum of their lengths.
    write(*,*) rect1%length + rect2%length
    
end subroutine do_rectangle_stuff

...

! instantiate an object of each type.
type(shape)     :: my_shape
type(rectangle) :: my_rectangle
type(square)    :: my_square

!do_rectangle_stuff( my_shape, my_shape )         ! Line 1
do_rectangle_stuff( my_rectangle, my_rectangle )  ! Line 2
do_rectangle_stuff( my_square, my_square )        ! Line 3
```

Line #1 is invalid since `shape` is not a `rectangle` and `do_rectangle_stuff()` specifies that it only takes `rectangle`-based types via `class(rectangle)`.  Line #3 works since `square` is a `rectangle` (as an extension of that type).
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

## Sourced Allocations (Cloning)
The `allocate()` statement accepts a `source=` argument which specifies the type and value the allocated object will have after allocation.

When using a sourced allocation, only one object can be allocated per call.

### Molded Allocations
Specifying the `source` argument sets the type and value of the source object.  Use the `mold` argument instead when one wants the type but not the value of the source object.

# Pointer Dimensionality
Pointers can have a different rank than the `target` they point to.  That is, a two-dimensional pointer can be associated with a one-dimensional `target` and indexing via the pointer accesses the associated linear position in the underlying array.

```fortran
integer, parameter :: N = 32
real, pointer      :: matrix(:, :)
real, allocatable  :: vector(:)

allocate( vector(N * N) )

matrix(1:N, 1:N) => vector
```

# User-defined Operators
## Using Custom Operators
Using a user-defined operator outside of the module that defines it requires knowing that the symbol name is of the form `operator(...)` rather than just the name of the operator.

```fortran
! SomeModule.f90
...
! define the binary operator "x", such that (a .x. b) is a valid expression.
interface operator(.x.)
    module procedure SomeModule_productVector
end interface
...

! code_using_SomeModule.f90
use SomeModule, only: operator(.x.)
```
