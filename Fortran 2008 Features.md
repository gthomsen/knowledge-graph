Tags: #software-engineering #fortran 

[NAG's summary of changes](https://www.nag.com/nagware/np/r62_doc/nag_f2008.html) introduced in Fortran 2008.

# Submodules
Submodules can be derived from modules to provide additional interface separation than introduced in Fortran95.

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

According to this [Intel Fortran Compiler community thread](https://community.intel.com/t5/Intel-Fortran-Compiler/CONTIGUOUS-attribute-for-dummy-arguments-what-happens-when-the/m-p/968361) the attribute specified contiguousness, but left ensuring that on the programmer.  The F2008 Corrigendum updated the Fortran 2008 specification so that the compiler would enforce contiguousness should situations arise where a `contiguous` and a non-`contiguous` array occurred in an expression.  In these cases, a temporary array is created to satisfy the `contiguous` requirements.

# Module Variables are Saved
According to the footnote in "Modern Fortran Explained" section 7.5.4, Fortran 2008 has the `save` attribute on all module data objects.

# Blocks
The `block`/`end block` construct allows for an executable region to be defined similar to an inline subroutine, though all of the host program's names are visible by default.  Duplicate names in a `block` hide the host's names.

# Procedure Pointers Can Point to Internal Methods
[[Fortran 2003 Features#Procedure Pointers|Procedure pointers]] can point to internal methods, rather than just external subprograms.