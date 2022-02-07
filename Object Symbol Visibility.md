Tags: #software-engineering #fortran 

Hidden symbols can cause unexpected errors during linking like so:

```shell
$ <linking command>
...
/usr/bin/ld: ../../libsimulation.a(Simulation_preRun.o): in function `__simulation_h_MOD_simulation_prerun':
/path/to/code/simulation/Simulation_preRun.f90:34: undefined reference to `__simulation_h_MOD_formatfilename'
```

Investigating `libsimulation.a` confirms that it has the `__simulation_h_MOD_formatfilename` symbol, though its visibility is limited to the local object (denoted by the little `t` in `nm`'s output) which prevents linking:

```shell
$ nm libsimulation.a | grep __simulation_h_MOD_formatfilename
                 U __simulation_h_MOD_formatfilename
                 U __simulation_h_MOD_formatfilename
                 U __simulation_h_MOD_formatfilename
00000000000012a2 t __simulation_h_MOD_formatfilename
```

Limited visibility can occur for a number of reasons:

1. (C/C++) The symbol was `static`
2. (C++) The symbol comes from code that was marked `private` (**NOTE:** Presumably, not verified)
3. (Fortran) The symbol comes from code that was marked `private`
4. The symbol comes from code that was explicitly marked as `hidden` and did not have any visibility attributes set to override.  This may occur during compilation or via a linker script during linking.

Once adjusting the symbols visibility, `nm` reports the symbol as visible (denoted by the big `T`) and linking occurs without error:
```shell
$ nm libsimulation.a | grep __simulation_h_MOD_formatfilename
                 U __simulation_h_MOD_formatfilename
                 U __simulation_h_MOD_formatfilename
                 U __simulation_h_MOD_formatfilename
00000000000012a2 T __simulation_h_MOD_formatfilename
```