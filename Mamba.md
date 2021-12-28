Tags: #conda #python 

Mamba is a Python wrapper for Conda that does its dependency resolution in C++.  Installing packages via Mamba is **orders** of magnitude faster and less likely to eventually fail (it should fail quickly when it does).

[Documentation](https://mamba.readthedocs.io/en/latest/index.html)

# Installation
**NOTE: As of 2021/12/26 it appears that non-`base` environment installs are [unsupported](https://mamba.readthedocs.io/en/latest/installation.html#installation).**
```shell
$ conda install -c conda-forge mamba
```
