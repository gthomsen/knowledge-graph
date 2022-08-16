Tags: #software-engineering #scientific-computing #hdf5 #fortran #debugging 

Linking a Fortran executable that uses the HDF5 library requires the inclusion of both the C ***AND*** the Fortran interface, otherwise one gets cryptic errors in the build log:

```shell
$ mpif90 -o nsem_replay communications.o constants.o grid.o main.o state.o -lhdf5_hl -lhdf5 -lz -lmpi -ldl
/usr/bin/ld: grid.o: warning: relocation against `__h5global_MOD_h5f_acc_rdonly_f' in read-only section `.text'
/usr/bin/ld: grid.o: in function `__grid_MOD_read_grid_from_initial_conditions':
/code/solver_surrogates/nsem_replay/grid.f90:77: undefined reference to `__h5global_MOD_h5f_acc_rdonly_f'
/usr/bin/ld: /code/solver_surrogates/nsem_replay/grid.f90:77: undefined reference to `__h5f_MOD_h5fopen_f'
/usr/bin/ld: warning: creating DT_TEXTREL in a PIE
collect2: error: ld returned 1 exit status
make: *** [Makefile:252: nsem_replay] Error 1
```

The above messages do not give obvious hints that  `libhdf5hl_fortran` and `libhdf5_fortran` are missing libraries in the link command.  The key indicators (obvious in hindsight) are the references to `__h5global_MOD_h5f_acc_rdonly_f` and `__h5f_MOD_h5fopen_f` which are not references to the user code, but rather the modules provided by the missing libraries.

Do ***NOT*** follow the red herring about position independent code indicated by `creating DT_TEXTREL in a PIE`!

The corrected command from above looks like:

```shell
$ mpif90 -o nsem_replay communications.o constants.o grid.o main.o state.o -lhdf5hl_fortran -lhdf5_fortran -lhdf5_hl -lhdf5 -lz -lmpi -ldl
```

