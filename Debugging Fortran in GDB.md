Tags: #fortran #scientific-computing #debugging

# Set the Language
Make sure to switch the language to Fortran, otherwise interpretation of symbols will not work as expected:
```
(gdb) set lang fortran
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