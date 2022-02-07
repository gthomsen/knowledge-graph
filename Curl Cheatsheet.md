Tags: #cheatsheet #utilities 

`curl` has a few options.  This cheatsheet is intended to avoid trawling through pages and pages of the manual when we want to use it.

# Download This File Here
The `-O` file takes the URL's basename (the last component) and uses that as the file name to write the contents to locally:
```shell
$ curl -O https://downloads.unidata.ucar.edu/netcdf-c/4.8.1/src/netcdf-c-4.8.1.tar.gz
$ ls -la netcdf-c-4.8.1.tar.gz
-rw-rw-r-- 1 user user 6602964 Feb  3 10:30 netcdf-c-4.8.1.tar.gz
```
