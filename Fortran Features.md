Collection of features that can't otherwise be attributed to a particular version.  Listed so they have referenceable names.

Mark Gates has a [decent reference](https://www.icl.utk.edu/~mgates3/docs/fortran.html) (CC-BY) which is more practical rather than repeating the standards.

# Array Initialization
Arrays can be initialized with a comma-delimited list of values, surrounded by slashes (`/`):
```fortran
real :: x(5) = / 1.0, 2.0, 3.0, 4.0, 5.0 /
```

It may also be enclosed in parentheses, though it is unclear when/if those are necessary:
```fortran
real :: x(5) = (/ 1.0, 2.0, 3.0, 4.0, 5.0 /)
```

Fortran 2003 [[Fortran 2003 Features#Array Initialization|allows the use of square brackets]] instead of the parentheses and slashes.

## Implied Do Syntax
Array values can be computed via an inline `DO` loop:
```fortran
integer :: n    = 5
real    :: x(n) = (/ (2*i, i=1, n) /) 
```

# Explicit vs Implicit Interfaces
Explicit interfaces are method declarations where all of the characteristics are known, including dummy arguments, their sequencing, their types, attributes of the method it self (e.g. `PURE` or `RECURSIVE`), etc.  These include:
- Methods within the current file (i.e. the entire file is parsed and compiled, so all interfaces contained are explicit)
- Methods from other modules that are used via `USE` (i.e. the module is explicitly queried about one of its interfaces)

Implicit interfaces are those that are external or are a dummy procedure.  Only the minimal information to invoke a method is known, which typically includes the number of arguments and their types.  These may be specified via:
- `EXTERNAL <external_name>`

# Actual vs Dummy Arguments
Actual arguments are those provided to a method (subroutine or function).  Dummy arguments are the names to the variables in the method's signature (think a physical dummy, e.g. a mannequin, as a standin for a person).

```fortran
subroutine do_stuff( dummy_int_argument, dummy_real_argument )
    integer, intent(in) :: dummy_int_argument
    real, intent(inout) :: dummy_real_argument

    dummy_real_argument = dummy_real_argument * dummy_int_argument
end subroutine do_stuff

integer :: n = 5
real    :: x = 1.5

do_stuff( n, x )
```

Anatomy of the above code:
- The subroutine `do_stuff` has two dummy arguments: 1) `dummy_int_argument` and 2) `dummy_real_argument`
- The host program provides two actual arguments to `do_stuff`: `n` is the actual argument for the dummy argument `dummy_int_argument`, and `x` is the actual argument for `dummy_real_argument`


