Tags: #software-engineering #fortran 

# Submodules
Submodules can be derived from modules to provide additional interface separation than introduced in Fortran 95.

See [[Fortran 2008 Submodules]] for more details.

# Contiguous Arrays
Previously, pointers and assumed-shape arrays could be associated with non-contiguous sequence of elements such as:

```fortran
vector(::2)           ! all odd-numbered elements
vector(10, 1, -1)     ! elements in reversed order
complex_array%real    ! real parts of a complex array
```

Previously, this had to be dealt with through additional bookkeeping and indexing which could prevent optimal implementations.

With the `contiguous` attribute both pointers and assumed-shape arrays must be contiguous, forcing the compiler to make temporary variables if necessary.

# Module Variables are Saved
According to the footnote in "Modern Fortran Explained" section 7.5.4, Fortran 2008 has the `save` attribute on all module data objects.

# Blocks
The `block`/`end block` construct allows for an executable region to be defined similar to an inline subroutine, though all of the host program's names are visible by default.  Duplicate names in a `block` hide the host's names.

# Procedure Pointers Can Point to Internal Methods
[[Fortran 2003 Features#Procedure Pointers|Procedure pointers]] can point to internal methods, rather than just external subprograms.