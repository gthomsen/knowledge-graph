Tags: #conda #python #scientific-computing 

Jupyter kernel that enables communication with non-Python code.  This is the foundation that the Jupyter debugger and ParaView kernels are built on.

[Documentation](https://xeus-python.readthedocs.io/en/latest/).  [Blog post](https://blog.jupyter.org/a-visual-debugger-for-jupyter-914e61716559) describing installation and gives a tour of its use.
 
# Installation
**NOTE: This may be out dated.  Last verified in the summer of 2021.**

Install the dependencies:
```shell
$ mamba install -c conda-forge cmake zeromq cppzmq OpenSSL xtl libuuid
```

Install Xeus and its Python interface:
```shell
$ mamba install -c conda-forge xeus xeus-python
```
