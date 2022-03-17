Tags: #scientific-computing 

Per the FFTW documentation, using multi-threaded FFTs with MPI requires a careful dance of initialization.  The sequence of events is:
1. `MPI_Init_thread()` with at least `MPI_THREAD_FUNNELED`
2. Verify that MPI's threading support is at least `MPI_THREAD_FUNNELED`
3. `fftw_init_threads()` to initialize FFTW's internal list of algorithms
4. `fftw_mpi_init()` to initialize FFTW's MPI components
5. Use threaded FFTW as normal
6. Optionally call `fftw_cleanup_threads()` to deallocate FFTW state along with per-thread state
7. Optionally call `fftw_mpi_cleanup()` to deallocate MPI-related FFTW state
8. Finish MPI operations via `MPI_Finalize`

From [FFTW's documentation](https://www.fftw.org/doc/Combining-MPI-and-Threads.html), the sequence looks like the following C code:
```c
int threads_ok;

int main( int argc, char **argv )
{
    int provided;
    MPI_Init_thread( &argc, &argv, MPI_THREAD_FUNNELED, &provided );
    threads_ok = (provided >= MPI_THREAD_FUNNELED);

    if( threads_ok )
    {
        threads_ok = fftw_init_threads();
    }
    fftw_mpi_init();

    ...
    if( threads_ok )
    {
        fftw_plan_with_nthreads(...);
    }
    ...

    fftw_cleanup_threads()
    fftw_mpi_cleanup()

    MPI_Finalize();
}
```

Of particular note, `fftw_cleanup()` does not also need to be called when calling either (or both) `fftw_cleanup_threads()` or `fftw_mpi_cleanup()`.  The [FFTW MPI initialization documentation](https://www.fftw.org/doc/MPI-Initialization.html) implies that `fftw_cleanup()` and `fftw_mpi_cleanup()` can both be called without ill effect, though I cannot find confirmation about `fftw_cleanup_threads()`.