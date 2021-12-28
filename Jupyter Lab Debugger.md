Tags: #jupyter #python #scientific-computing 

Once installed, the debugger is available via the 

# Installation
**NOTE: This may be outdated.  This worked during summer of 2021.**

This assumes [[Mamba]] has been installed.

Install the Node.js dependency:
```shell
$ mamba install nodejs -c conda-forge
```

Install several extensions to setup the Lab interface (Lab Manager, Lab-Matplotlib integration) and the dependency to glue Matplotlib together:
```shell
$ jupyter labextension install @jupyter-widgets/jupyterlab-manager
$ jupyter labextension install jupyter-matplotlib
$ jupyter nbextension enable --py widgetsnbextension

# for inline Matplotlib figures in Jupyter lab.
$ conda install -c conda-forge ipympl
```

Install ![[Xeus#Installation]].

# Debugging
The debugger can only be used on Notebooks that are run with the XPython kernel (standard Python kernel with Xeus support).  

Clicking the bug icon in the top-right of the Lab enables the debugger and allows you to manage breakpoints and inspect variables:

![[resources/jupyter-lab-debugger-icon.png]]

