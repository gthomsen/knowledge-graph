Tags: #linux 

# Enforcement Level
SELinux can be disabled, permissive (checked and violates are logged), or enforced.  Debugging should start by determining which level the system is in:

```
$ getenforce
```

If the above command doesn't exist, then SELinux isn't installed.