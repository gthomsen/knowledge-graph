Tags: #scientific-computing #benchmarking 

Planning doesn't really matter for small (`nfft`<128) 1D FFTs unless they're batched.  Once batched, then more patient planning (`FFTW_MEASURE` and `FFTW_PATIENT`) results in up to 2x performance gains.