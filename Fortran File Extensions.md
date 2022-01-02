Tags: #fortran #scientific-computing 

**NOTE:** This [link](https://software.intel.com/en-us/forums/intel-fortran-compiler-for-linux-and-mac-os-x/topic/328744) worked back in 2017 to provide evidence to the claim below, though does not appear to work in 2022.

The Fortran standards do not specify particular filename extensions for source code.  `.f90` was widely adopted as free-form source in most compilers (GFortran, IFort, etc), though one should specify the standard a unit is being compiled against on the command line to be safe.