Tags: #software-engineering #scientific-computing #compiler-optimizations 

GNU compilers support the `-march=native` option to target optimizations for the system's CPU architecture.  One question you might ask is, which architecture did it select?  This is not-obvious given that older compilers still function on processors created after the compiler was released.  

Requesting the target's help (`--target-help`) while providing the query option first (`-Q`) reports the architecture selected by `-march=native`:
```shell
$ gfortran -Q --target-help -march=native | grep 'march=  '
march=znver1
```

Note how removing `-march=native` changes the architecture:
```shell
$ gfortran -Q --target-help -march=native | grep 'march=  '
march=x86-64
```

It's worth pointing out that `-Q --target-help` lists *all* of the options currently selected, as well as their enabled/disabled status:
```shell
$ gfortran -Q --target-help -march=native | grep avx
  -mavx                                 [enabled]
  -mavx2                                [enabled]
  -mavx256-split-unaligned-load         [disabled]
  -mavx256-split-unaligned-store        [enabled]
  -mavx5124fmaps                        [disabled]
  -mavx5124vnniw                        [disabled]
  -mavx512bw                            [enabled]
  -mavx512cd                            [enabled]
  -mavx512dq                            [enabled]
...
```