Tags: #mpi

Debugging and profiling MPI applications occasionally needs to identify which MPI rank is executing from the environment (e.g. from within a shell script).  This is MPI distribution dependent - see the environment variables below.

# OpenMPI
`OMPI_COMM_WORLD_RANK` holds the rank index and `OMPI_COMM_WORLD_SIZE` holds the world size.
# Intel MPI
`PMI_RANK` holds the rank index and `PMI_SIZE` holds the world size.