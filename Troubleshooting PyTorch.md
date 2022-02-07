Tags: #python 

```python
# NOTE: change the python3.9 component to match the installation.
$ python ${CONDA_PREFIX}/lib/python3.9/site-packages/torch/utils/collect
```

# Verify CUDA is Available
Torch provides a simple method to report whether CUDA is currently available.  

```python
>>> torch.cuda.is_available()
False
```

When it reports `False` this may be due to a number of factors:
- No GPU devices are visible
- The GPU driver is not loaded
- The user does not have permission to access the GPU
- PyTorch was not compiled with CUDA support

Attempting to initialize CUDA will provide a clue as to why support is unavailable:

```python
>>> torch.cuda.init()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/opt/miniconda3/envs/base/lib/python3.9/site-packages/torch/cuda/__init__.py", line 185, in init
    _lazy_init()
  File "/opt/miniconda3/envs/base/lib/python3.9/site-packages/torch/cuda/__init__.py", line 208, in _lazy_init
    raise AssertionError("Torch not compiled with CUDA enabled")
AssertionError: Torch not compiled with CUDA enabled
```