Tags: #scientific-computing #unfinished #benchmarking

libxsmm provides a standalone benchmarking tool to measure various matrix-matrix multiplication implementations.  Allows testing of streaming arguments (nothing is reused), fixed and streamed arguments, and batched execution.  Sizes and counts can be specified, and it shows sampled FLOPS, computed bandwidth, and measured duration (in miliseconds).

[Documentation](https://libxsmm.readthedocs.io/en/latest/libxsmm_samples/#smm-sample-collection) on the sample that provides the tool.

# Command Line

Once [[#Building]] is complete, running individual benchmarks is done via:

```shell
# run 10,000 iterations of a (36x28) = (36x38) * (38x28) matrix multiplication benchmark.
$ samples/smm/specialized.sh 0 36 28 38 10000
m=36 n=28 k=38 size=10000 memory=262.5 MB (input=f64 output=f64)

Batched (A,B,C)...
        pseudo-perf.: 7.0 FLOPS/cycle
        performance: 21.2 GFLOPS/s
        bandwidth: 9.2 GB/s
        duration: 36 ms
Indirect (A,B,C)...
        pseudo-perf.: 7.0 FLOPS/cycle
        performance: 21.2 GFLOPS/s
        bandwidth: 9.2 GB/s
        duration: 36 ms
Finished
```

`specialized.sh` takes multiple parameters:
1. Benchmark mode XXX: get modes
2. `M` - number of rows in `A`
3. `N` - number of columns in `C`, columns in `B`
4. `K` - Number of columns in `A`, rows in `B`
5. Count requested. ***NOTE:*** This is capped so the benchmark fits into 2 GiB by default.

# Building
```shell
#
# NOTE: adjust AVX= according to the target system.
#
$ make AVX=2
$ make -C samples/smm/
```
