Tags: #utilities #ssh 

# Enumerating Client Capabilities

```shell
$ ssh -Q kex
diffie-hellman-group1-sha1
...
```

# Specifying Custom Capabilities on Command Line
```shell
$ ssh user@host
Unable to negotiate with host port 22: no matching key exchange method found. Their offer: diffie-hellman-group1-sha1
$ ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 user@host
```