Tags: #unfinished 
```shell
$ mpif90 -cpp -c  -O0 -Jbuild-gfortran7.5-OPTIMIZE/modules -fopenmp -std=f2008 -Wall -Wextra -Wno-c-binding-type -Wno-maybe-uninitialized -DUSE_FFTW -DUSE_NETCDF -I/opt/include -I/opt/include -I/opt/include  problems/djl_solitary_wave_yz/djl_solitary_wave_yz_initialConditions.f90 -o build-gfortran7.5-OPTIMIZE//problems/djl_solitary_wave_yz/djl_solitary_wave_yz_initialConditions.o
*** buffer overflow detected ***: /usr/lib/gcc/x86_64-linux-gnu/7/f951 terminated
f951: internal compiler error: Aborted
Please submit a full bug report,
with preprocessed source if appropriate.
See <file:///usr/share/doc/gcc-7/README.Bugs> for instructions.
problems/problems.mk:29: recipe for target 'build-gfortran7.5-OPTIMIZE//problems/djl_solitary_wave_yz/djl_solitary_wave_yz_initialConditions.o' failed
```