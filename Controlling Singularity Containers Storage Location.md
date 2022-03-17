Tags: #utilities #containers #linux 

Singularity uses a SquashFS-based file for its container images and can convert "normal" layered OCI images into a single `.sif` file.  While the user can specify where the final image is stored, the intermediate files (both temporary and cache) default to `${TMPDIR}` and `${HOME}/.singularity/cache`.

Specifying new locations for the temporary build location as well as the cache can be done via the following environment variables:
```shell
$ export SINGULARITY_TMPDIR=/path/to/scratch
$ export SINGULARITY_CACHEDIR=/path/to/cache
```