Tags: #linux #benchmarking 

Clearing the page forces any previously cached files to be re-read on their next access.

Can clear them via `sysctl`:
```shell
$ sudo sysctl vm.drop_caches = 1
```

Or clear them via `/proc/`:
```shell
# echo 1 > /proc/sys/vm/drop_caches
```