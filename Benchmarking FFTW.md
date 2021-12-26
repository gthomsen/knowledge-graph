Tags: #scientific-computing #benchmarking 

FFTW provides a benchmark tool as part of their testing suite that measures different FFT sizes.  Can handle arbitrary dimensions (assumed, I've tested 1D and 2D) as well as batches (N-many 1D FFTs) and respects the planning type.

# Command Line

```shell
# compute 2940 (60*7*7) 128-point real to complex transforms, out of place.
$ tests/bench -v2 -o patient or128*2940
planner time: 0.807861 s
(rdft2-ct-dit/2
  (hc2c-direct-2/4/1-x2940 "hc2cfdftv_2_avx2_128"
    (rdft2-r2hc-direct-2 "r2cf_2")
    (rdft2-r2hc01-direct-2 "r2cfII_2"))
  (dft-direct-64-x2940 "n1fv_64_avx2_128"))
flops: 429240 add, 176400 mul, 467460 fma
estimated cost: 1546440.000000, pcost = 1138408.000000
Problem: r128*2940, setup: 807.92 ms, time: 381.34 us, ``mflops'': 17269.458
Took 8 measurements for at least 10.00 ms each.
Time: min 381.34 us, max 416.00 us, avg 398.05 us, median 392.81 us
```

Follows `fftw-wisdom`'s command line syntax (for the most part).  Some examples:

- `or128`: Out of place, real 128-point FFTs
- `ir1024*2000`: Batch of 2000 in place, real 1024-point FFTs