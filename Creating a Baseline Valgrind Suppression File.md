Tags: #software-engineering #unfinished 

Workflow:
1. Generate baseline findings
2. Edit baseline - remove non-rules and simplify rules

```shell
# NOTE: can also supply --suppressions=/path/to/existing/suppressions to
#       incrementally build up a baseline.
$ valgrind \
    --leak-check=full \
    --error-limit=no \
    --gen-suppressions=all \
    --log-file=suppressions.log \
    application args
```

# Running with Suppressions
```shell
$ valgrind \
    --leak-check=full \
    --error-limit=no \
    --show-error-list=yes \
    --suppressions=baseline.suppressions \
    application args
```

# Suppression File Format
Comments are started with `#`, empty lines are ignored.

Collection of one or more stack descriptors:
```
{
   <16 bytes in mca_btl_base_select()>
   Memcheck:Leak
   match-leak-kinds: definite
   fun:malloc
   ...
   fun:mca_bml_base_init
   fun:ompi_mpi_init
   fun:PMPI_Init_thread
   fun:MPI_INIT_THREAD
   fun:mpi_init_thread_f08_
   fun:MAIN__
   fun:main
}
```

Descriptors have the following format:
```
{
   Rule name
   Memcheck:Leak                 # other Valgrind tools can be specified.
   match-leak-kinds: definite    # rules can include certainty of the leak.
   fun: malloc                   # name of the function that produced the leak.
   ...                           # wildcard that matches zero or more intermediate
                                 # frames.
   fun: <function>               # one or more <functions>, possibly with wildcards,
                                 # to match against.
   fun: main                     # top-level function to match against.
}
```

## References
Valgrind documentation for [writing suppression files](https://valgrind.org/docs/manual/mc-manual.html#mc-manual.suppfiles).  Documentation on [suppressing errors](https://valgrind.org/docs/manual/manual-core.html#manual-core.suppress) also has additional information.
