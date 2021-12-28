Tags: #conda #python 

Cloning an environment from another uses `conda create`:
```shell
$ conda create --name new-environment --clone base
```

Creating an environment from an `environment.yml` uses `conda env`:
```shell
$ conda env create -f /path/to/environment.yml
```

Naming an environment created from `environment.yml` is harder: ![[Conda Quirks#Naming Environments]]