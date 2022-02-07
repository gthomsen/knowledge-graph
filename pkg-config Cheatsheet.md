Tags: #linux #cheatsheet #utilities 

# Updating Search Path
`PKG_CONFIG_PATH` is a colon-delimited list of directories to search for `.pc` files.  Adjust this when installing user-specific software.

# List Available Packages
Enumerate packages on the system:
```shell
$ pkg-config --list-all | sort | head
adwaita-icon-theme             gnome-icon-theme - A collection of icons used as the basis for GNOME themes
applewmproto                   AppleWMProto - AppleWM extension headers
arpack                         ARPACK-NG - Collection of Fortran77 subroutines designed to solve large scale eigenvalue problems
bash-completion                bash-completion - programmable completion for the bash shell
bigreqsproto                   BigReqsProto - BigReqs extension headers
blas-netlib                    BLAS - FORTRAN reference implementation of BLAS Basic Linear Algebra Subprograms
blas                           openblas-blas - Optimized BLAS (linear algebra) library based on GotoBLAS2
caf-openmpi                    CAF - Co-Array Fortran support
```

# Querying Build and Link Flags
Report how to build and link against a particular package with `--cflags` and `--libs`, respectively:
```shell
$ pkg-config --cflags python-3.8
-I/usr/include/python3.8 -I/usr/include/x86_64-linux-gnu/python3.8
$ pkg-config --libs python-3.8
```