Tags: #fortran #scientific-computing #debugging

# Set the Language
Make sure to switch the language to Fortran, otherwise interpretation of symbols will not work as expected:
```
(gdb) set lang fortran
```

# Breakpoint Conditionals
Conditionals are specified in the current language.  For example, stopping at a breakpoint when two values do not equal each other requires the use of `.ne.`:
```
(gdb) break foo.f90:1234
Breakpoint 1 at 0x561bd3bfa857: file foo.f90, line 1234.
(gdb) cond 1 (value1 .ne. value2) 
```

# Function Return Values
Inspecting results returned from a function from within said function is not as simple as printing the named variable.   Consider the following:
```fortran
function my_op( x, y ) result( z )
    real, intent(in) :: x, y
    real             :: z

    z = x * y   ! line 1
end function my_op
```

Breaking at line #1 and attempting to inspect `z` results in an error:
```
(gdb) print z
No symbol "z" in current context.
```

This is due to the fact that functions conform to some ABI and pass the result as an additional argument, with a mangled name.  Inspecting the function's arguments reveals this fact and allows interaction with the mangled name:
```
(gdb) info args
__z = 0.0
(gdb) print __z
$1 = 0.0
```

# Fortran Modules
Modules act as a namespace and need to be qualified when referenced from within GDB.

Consider the following code:
```fortran
from tranverse, only:   cy
```

Inspecting the variable in GDB requires `transverse::cy` and not `cy`:
```
(gdb) print cy
No symbol "cy" in current context.
(gdb) print transverse::cy
$1 = <not allocated>
```

That said, if one knows the name mangling scheme used variables can be accessed anywhere in the program, regardless of whether the module (`transverse` above) was used in the current scope or not.  Note that accessing the symbol requires casting it to the appropriate type as GDB doesn't (sometimes?) know that information.  The following assumes a `__<module>_MOD_<name>` mangling scheme (this is found with GNU gfortran):
```
(gdb) p (integer)__transverse_mod_cy
128
```

# Derived Types
GDB does not appear to inspect objects as if they're Fortran objects, but rather exposes the underlying C implementation.  This requires additional effort to typecast and dereference objects of interest.
```
(gdb) p *(custom_type*)(this%_data)
$1 = ( map = ( c_keys = <not allocated> ), i_values = (0, 0) )
```

**NOTE:** The [[#Set the Language|language must be set]] before running the above.  Without that, GDB will complain about not having `custom_type` in the current context:
```
(gdb) p *(custom_type*)(this%_data)
No symbol "custom_type" in the current context.
```

# Printing Type Information
Given Fortran's `kind` system, it's not always clear as to the type of a particular symbol. Use `whatis` to determine that at run-time:
```
(gdb) whatis mpi::MPI_DOUBLE_PRECISION
type = integer(kind=4)
```

## Derived Types
Understanding which [[#Derived Types|derived type you're inspecting]] is key when working with submodules since print the Fortran variable gives the implementation-specific structure:
```fortran
(gdb) p this
this = ( _data = 0x5555556c8560, _vptr = 0x5555555576760 <_filename_MOD__vtab_filename_typename> )
```

The `_data` pointer holds the variable's contents, though it does not hint at its type.  While one could inspect `_vptr` to determine the underlying type, it is mangled (`_filename_MOD__vtab_filename_typename` in this case). Both `whatis` and `ptype` help out:
```
(gdb) whatis this
type = Type __class_filename_typename
(gdb) ptype this
type = Type __class_filename_typename
    PTR TO -> ( Type typename :: _data )
    PTR TO -> ( Type __vtype_filename_typename :: _vptr)
End Type __class_filename_typename
```

# Invoking Intrinsics
The functions implementing language intrinsics (e.g. `size()` or `allocated()`) are compiler specific, and can (likely) have different names.  This makes calling them from within GDB challenging as it requires investigation.

## gfortran Intrinsics
Tag: #unfinished 
Libraries used by `gfortran` include:
- `libgfortran.so`
- `libgcc_s.so`

`libgfortran.so` calls `_gfortran_runtime_error_at()` when a run-time error occurs, so setting a breakpoint on it allows inspecting program state before it exits:
```
(gdb) break _gfortran_runtime_error_at
(gdb) run
...
Thread 6 "foo.x" hit Breakpoint 1, 0x00007f7ec0107990 in _gfortran_runtime_error_at () from /lib/x86_64-linux-gnu/libgfortran.so.5
```

# Serializing Variables to Disk
Writing arrays to disk so they can be visualized externally is a critical tool when debugging algorithm implementations and GDB's `dump` command allows one to do it.  Care needs to be taken to take the address of a particular variable or array entry via the `&` operator like so:

```gdb
(gdb) dump binary memory foo.bin &array &array(256, 16)
```

Watch out for the oh-so-helpful `Value can't be converted to integer.` message if you don't specify the address of a variable:
```gdb
(gdb) dump binary memory foo.bin variable(1, 1) variable(256, 16)
Value can't be converted to integer.
```

***NOTE:*** You may have to set `max-value-size` to a sufficiently large number (or `unlimited`) to serialize large arrays, like so:
```gdb
(gdb) set max-value-size unlimited
```

***NOTE:*** Dumping a 1D array using its upper bound index will produces a file with one less element in it:

```
# this produces a file with 10239 elements!
(gdb) dump binary memory foo.bin &array_1D &array_1D(10240)
```

To get all of the elements, use an offset relative to the first index:
```
(gdb) dump binary memory foo.bin &array_1D &array_1D + 10240
```

# Stopping the Debugger at a Fortran Run-time Error
Both gfortran and ifort allow for run-time validation to aide in development and debugging.  One can cause the debugger to stop when a run-time error is encountered by setting a breakpoint on a compiler-specific routine.

## GDB
Set a breakpoint on the `_gfortran_runtime_error_at` symbol to stop after the error has been encountered:

```gdb
(gdb) break _gfortran_runtime_error_at
Breakpoint 1 at 0x7f123fc0c8b0
(gdb) continue
Thread 1 "nsem_particle_t" hit Breakpoint 1, 0x00007f123fc0c8b0 in _gfortran_runtime_error_at () from /usr/lib/x86_64-linux-gnu/ligfortran.so.5
(gdb) where
#0  0x00007f123fc0c8b0 in _gfortran_runtime_error_at ()
   from /usr/lib/x86_64-linux-gnu/libgfortran.so.5
#1  0x000055b63ac9afc0 in scatter::extract_local_grid (
    solver_grid_x=<error reading variable: value requires 1272384 bytes, which is more than max-value-size>,
    solver_grid_y=<error reading variable: value requires 1272384 bytes, which is more than max-value-size>,
    solver_grid_z=<error reading variable: value requires 1272384 bytes, which is more than max-value-size>) at Solver.f90:312
#2  0x000055b63ac8df44 in driver () at Driver.f90:207
#3  0x000055b63ac8ebed in main (argc=1, argv=0x7fff540f8098) at Driver.f90:3
#4  0x00007f123f8d6565 in __libc_start_main ()
   from /usr/lib/86_64-linux-gnu/libc.so.6
#5  0x000055b63ac8d44e in _start ()
```

The program threw a run-time error at `Solver.f90:312` and can be debugged as normal.

# Investigating State
```
(gdb) info module variables
(gdb) info module functions
```

# Calling C Interfaces from Fortran
Variables/parameters are interpreted differently when calling C interfaces depending on the source language.  Calling a C routine from within GDB requires changing the source language to C to avoid surprising behavior, including:
1. Symbol name case changes
2. XXX

For a C interface like so:
```c
int locate_nans_f64( double *double_array, int number_elements );
```

Calling  `locate_nans_f64()` with Fortran as the current language will result in the following:
```gdb
(gdb) call locate_nans_f64( &Nrhoh2vect, 184320 )
No symbol "Nrhoh2vect" in current context.
```

This is because Fortran symbols are implicitly lower-cased and `Nrhoh2vect` does not exist in the binary, though `nrhoh2vect` does.  Changing the case does not work and results in the following:
```gdb
(gdb) call locate_nans_f64( &nrhoh2vect, 184320 )
Empty region supplied.
$1 = 0
```

The `Empty region supplied` message only appears if the 2nd argument is not positive which means the length parameter (`184320`) is incorrectly interpreted (i.e. as a negative value).  Changing the language to C to match the interface results in the correct behavior:
```gdb
(gdb) set language c
(gdb) call locate_nans_f64( &nrhoh2vect, 184320 )
$1 = 0
```