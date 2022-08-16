Tags: #tools #debugging #performance

It appears that Valgrind sometimes does not play nicely with `gprof`.   While the subordinate program may run, it might not terminate due to `SIGPROF` being delivered indicating that the `gmon.out` profiling file needs to be written.  This looks like the following:

```
==3053== Process terminating with default action of signal 27 (SIGPROF)
==3053==    at 0x4EF601A: __open_nocancel (open64_nocancel.c:45)
==3053==    by 0x4F0314F: write_gmon (gmon.c:370)
==3053==    by 0x4F039BE: _mcleanup (gmon.c:444)
==3053==    by 0x4E2D87D: __cxa_finalize (cxa_finalize.c:83)
==3053==    by 0x10A596: ??? (in /code/NodalSEM_INSE/particle_tracking_mex/nsem_particle_tracker)
==3053==    by 0x4019D52: _dl_fini (dl-fini.c:139)
==3053==    by 0x4E2D146: __run_exit_handlers (exit.c:108)
==3053==    by 0x4E2D2EF: exit (exit.c:139)
==3053==    by 0x4E1156B: (below main) (libc-start.c:366)
```