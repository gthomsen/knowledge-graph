Tags: #scientific-computing #python

# Naming Environments
You can't create a Conda environment by name that differs from what is in `environment.yml`. At best you can specify the full path to a new environment like so:

```shell
# overrides the environment name from environment.yml with 'foo'.
$ conda env create -f python/environment.yml -p ${CONDA_ENV}/envs/foo
```
