Tags: #linux #performance #scientific-computing 

For the occasion where a system has simultaneous multithreading (SMT), hyperthreading (HT) in Intel's world, enabled but the target application does not benefit from it, the `sysfs` file `/sys/devices/system/cpu/cpuN/topology/thread_siblings_list` has a list of sibling cores that share execution resources.  CPU cores are specified by index (0-based).  This is useful for identifying which cores to restrict an application to so there is no resource contention during execution.

```shell
# show the sibling cores for the second core on an 8-core, 16-thread, system:
$ cat /sys/devices/system/cpu/cpu1/topology/thread_siblings_list
1,9
```

`lscpu` can also report the CPU to core mapping for every core on the system:
```shell
$ lscpu -p
# The following is the parsable format, which can be fed to other
# programs. Each different item in every column has an unique ID
# starting usually from zero.
# CPU,Core,Socket,Node,,L1d,L1i,L2,L3
0,0,0,0,,0,0,0,0
1,1,0,0,,1,1,1,0
2,2,0,0,,2,2,2,0
3,3,0,0,,3,3,3,0
4,4,0,0,,4,4,4,1
5,5,0,0,,5,5,5,1
6,6,0,0,,6,6,6,1
7,7,0,0,,7,7,7,1
8,0,0,0,,0,0,0,0
9,1,0,0,,1,1,1,0
10,2,0,0,,2,2,2,0
11,3,0,0,,3,3,3,0
12,4,0,0,,4,4,4,1
13,5,0,0,,5,5,5,1
14,6,0,0,,6,6,6,1
15,7,0,0,,7,7,7,1
```

In the above example the second column ("Core") indicates the physical core while the first column ("CPU") specifies the logical CPU reported by the OS (as used by `taskset`).