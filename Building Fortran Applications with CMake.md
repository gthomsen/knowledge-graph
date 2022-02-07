Tags: #software-engineering #fortran #scientific-computing 

[[Fortran 2008 Submodules|Submodules]] require two-pass processing to dynamically detect dependencies.

[Detailed description](https://mathstuf.fedorapeople.org/fortran-modules/fortran-modules.html) of how CMake pre-processes, scans, collates, and compiles Fortran code in parallel while respecting dynamically discovered dependencies:

![CMake Fortran Build Graph](https://mathstuf.fedorapeople.org/fortran-modules/graph-single-target-after.png)

["Hello World"-style example](https://gitlab.kitware.com/cmake/community/-/wikis/doc/cmake/languages/fortran/ForFortranExample) building a Fortran application in CMake.  Requires at least CMake v2.6 (released circa 2008).