Tags: #fortran #scientific-computing #debugging

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

# Printing Type Information
Given Fortran's `kind` system, it's not always clear as to the type of a particular symbol. Use `whatis` to determine that at run-time:
```
(gdb) whatis mpi::MPI_DOUBLE_PRECISION
type = integer(kind=4)
```
