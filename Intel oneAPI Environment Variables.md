Tags: #software-engineering 

Configuring the entire oneAPI suite is simple:
```shell
$ source ${ONEAPI_ROOT}/setvars.sh
```

The above adds the following into the environment:
- `clck` - ?
- `compiler` - C/C++ (`icc` and `icpc`) and Fortran compilers (`ifort`)
- `debugger` - oneAPI-enabled GDB
- `dev-utilities` - Eclipse tools
- `inspector` - Intel Inspector
- `itac` - Intel Trace Analyzer and Collector
- `mpi` - Intel MPI
- `tbb` - Thread Building Blocks

Individual components can be added to the environment, one by one via `source ${ONEAPI_ROOT}/<component>/latest/env/vars.sh`, where `<component>` is one of the above.  

For example, loading just the compilers and debuggers:
```shell
$ source ${ONEAPI_ROOT}/compiler/latest/env/vars.sh
$ source ${ONEAPI_ROOT}/debugger/latest/env/vars.sh
```