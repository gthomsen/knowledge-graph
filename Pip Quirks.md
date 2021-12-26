Tags: #python 

# Random Hangs When Remotely Logged into Desktop
Tags: #linux 

Pip sometimes attempts to query a keyring agent running on the desktop which hangs the action in the remote session.  The following prevents this inadvertant association:

```shell
$ export PYTHON_KEYRING_BACKEND=keyring.backends.null.Keyring
```
