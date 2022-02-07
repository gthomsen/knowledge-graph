Tags: #python 

# Random Hangs When Remotely Logged into Desktop
Tags: #linux 

Pip sometimes attempts to query a keyring agent running on the desktop which hangs the action in the remote session.  This is not apparent from the following output when installing a package:

```shell
$ pip install some_package
Looking in indexes: https://pypi.org/simple
```

The following prevents this inadvertent association:

```shell
$ export PYTHON_KEYRING_BACKEND=keyring.backends.null.Keyring
```

Increasing the verbosity during installation will give a clue that the keyring needs to be disabled:

```shell
Using pip 20.2.4 from /home/user/anaconda3/envs/base/lib/python3.8/site-packages/pip (python 3.8)
Non-user install because site-packages writeable
Created temporary directory: /tmp/pip-ephem-wheel-cache-ex26asuf
Created temporary directory: /tmp/pip-req-tracker-t542orbv
Initialized build tracking at /tmp/pip-req-tracker-t542orbv
Created build tracker: /tmp/pip-req-tracker-t542orbv
Entered build tracker: /tmp/pip-req-tracker-t542orbv
Created temporary directory: /tmp/pip-install-cuxh9j1i
Looking in indexes: https://pypi.org/simple
1 location(s) to search for versions of some_package:
* https://pypi.org/simple/some_package/
Fetching project page and analyzing links: https://pypi.org/simple/some_package/
Getting page https://pypi.org/simple/some_package/
Found index url https://pypi.org/simple
Getting credentials from keyring for https://pypi.org/simple
```