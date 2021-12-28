Tags: #linux #utilities #gpu

NVIDIA GPU power draw can be softly limited via `nvidia-smi`.  Sometimes the draw will exceed the threshold which will result in throttling the GPU.  Depending on the computations, this can result in wild variance in throughput and latencies.

Set a power threshold until the next reboot:
```shell
# set a 125W power threshold.
$ sudo nvidia-smi -pl 125
```