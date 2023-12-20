Tags: #mpi #scientific-computing 

Environment variables can be inherited from the calling process (the default as of Intel MPI 2021.9.0), or specified via the  `-genv VARIABLE=value`  option to `mpirun` and `mpiexec`.

Debug information can be printed by setting the `I_MPI_DEBUG` variable, and the nodes selected are available at level 4:
```
$ mpirun -genv I_MPI_DEBUG=4 -n 1 ./mpi_application.x
```

Details about the environment variables are printed at level 5:
```
$ mpirun -genv I_MPI_DEBUG=5 -n 1 ./mpi_application.x
        [0] MPI startup(): Intel(R) MPI Library, Version 2021.9  Build 20230307 (id: d82b3071db)
        [0] MPI startup(): Copyright (C) 2003-2023 Intel Corporation.  All rights reserved.
        [0] MPI startup(): library kind: release
        [0] MPI startup(): libfabric version: 1.13.2rc1-impi
        [0] MPI startup(): libfabric provider: mlx
        [0] MPI startup(): Load tuning file: "/p/app/compilers/intel/intel-hpckit/2023.1.0-46346/mpi/2021.9.0/etc/tuning_generic_shm-ofi_mlx_hcoll.dat"
        [0] MPI startup(): Rank    Pid      Node name                     Pin cpu
        [0] MPI startup(): 0       1980496  node_name                     {0}
        [0] MPI startup(): I_MPI_ROOT=/p/app/compilers/intel/intel-hpckit/2023.1.0-46346/mpi/2021.9.0
        [0] MPI startup(): I_MPI_MPIRUN=mpirun
        [0] MPI startup(): I_MPI_HYDRA_TOPOLIB=hwloc
        [0] MPI startup(): I_MPI_HYDRA_BOOTSTRAP=slurm
        [0] MPI startup(): I_MPI_PIN_UNIT=-1
        [0] MPI startup(): I_MPI_PIN=off
        [0] MPI startup(): I_MPI_PIN_PROCESSOR_LIST=1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64
        [0] MPI startup(): I_MPI_INTERNAL_MEM_POLICY=default
        [0] MPI startup(): I_MPI_DEBUG=5
```