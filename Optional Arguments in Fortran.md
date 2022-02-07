Tags: #software-engineering #fortran 

Optional arguments to a subprogram can be queried via the `present()` method:

```fortran
subroutine optional_arguments( required_argument, optional_argument )

    integer, intent(in)           :: required_argument
    integer, optional, intent(in) :: optional_argument

    if present( optional_argument ) then
        ! do one thing with optional_argument.
    else
        ! do another thing without optional_argument.
    endif
    ...
```