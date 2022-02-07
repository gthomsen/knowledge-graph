Tags: #software-engineering #fortran #scientific-computing 

Command line parsing in Fortran is a serious headache prior to Fortran 2003.  Both `get_command_argument()` and `command_argument_count()` were added in Fortran 2003, and the former does not take [[Strings in Fortran#Deferred Length Allocations|deferred length allocations]]. 

As a result, the following is required to parse arbitrary command line arguments:

```fortran
integer                       :: argument_index
integer                       :: argument_length
character(len=:), allocatable :: argument

! assumes argument_index is set to the argument of interest.
get_command_argument( argument_index, length=argument_length )
allocate( character(argument_length) :: argument )
get_command_argument( argument_index, value=argument )
```