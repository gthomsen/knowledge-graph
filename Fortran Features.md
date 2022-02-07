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