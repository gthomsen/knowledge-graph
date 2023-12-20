Tags: #software-engineering #fortran 

Adding the `-h display_opt` option to the Cray compilers (C/C++, Fortran) causes the compiler to report the configuration it is using in terms of the corresponding command line flags.  Since some shorthand flags (e.g. `-O3`) expand to a number of other flags, this is nice to see the mapping without studying the man page:

```shell
ftn -c  -G 2 -O3 -h align_arrays -h autoprefetch -h cblock2 -h fma -h nofp_trap -h ipa3 -h page_align_allocate -h vector2 -e o -h display_opt -J build-crayftn12.0.3-DEBUG_no-OPENMP_yes/modules -e T -h omp -e C -e n -h alias=none -h noautothread -DUSE_FFTW -DUSE_NETCDF -I/opt/cray/pe/fftw/3.3.8.11/x86_rome/include -I/opt/cray/pe/netcdf-hdf5parallel/4.7.4.7/include -I/opt/cray/pe/hdf5-parallel/1.12.0.7/include  src/grid/Grid_h.f90 -o build-crayftn12.0.3-DEBUG_no-OPENMP_yes/src/grid/Grid_h.o
Options: -h scalar3,vector2,unroll2,fusion2,cache0,cblock2,noaggress
         -h ipa3,mpi0,pattern,modinline
         -h fp3=approx,flex_mp=default,alias=none:standard_restrict
         -h fma
         -h autoprefetch,noconcurrent,nooverindex,shortcircuit2
         -h noadd_paren,nozeroinc,noheap_allocate
         -h align_arrays,page_align_allocate,nocontiguous,nocontiguous_pointer
         -h nocontiguous_assumed_shape
         -h thread2,nothread_do_concurrent,noautothread,safe_addr
         -h omp,caf,noacc
         -h nofunc_trace,noomp_analyze,noomp_trace,nopat_trace
         -h nobounds
         -h nomsgs,nonegmsgs,novector_classic
         -h dynamic (or -dynamic)
         -h cpu=x86-64,x86-rome,network=slingshot10
         -h nofp_trap -K trap=none
         -s default32 -G2
         -e noCT (user_specified)
         -d 0abcdefgijpvxzBDEGINPQSZ (default)
         -e hmqwAFKRX (default)
         -J uild-crayftn12.0.3-DEBUG_no-OPENMP_yes/modules

Notes:   -e n is "Enable ansi messages"
         -e o is "Display commandline option information"
         -e C is "Standard call site checking"
         -e T is "Preprocess"
```
