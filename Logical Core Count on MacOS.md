Tags: #utilities #macos 

Programmatically get the number of cores on the system for shell scripting:

```shell
$ NUMBER_CORES=`sysctl -n hw.ncpu`
```

This replaces the quick-and-dirty logical core count on Linux:

```shell
$ NUMBER_CORES=`grep MHz /proc/cpuinfo | wc -l`
```