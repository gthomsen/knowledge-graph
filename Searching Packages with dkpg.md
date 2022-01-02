Tags: #ubuntu #linux #utilities 

# Identify a File's Package
When investigating an issue it is helpful to map a file to the package that owns/installs it for further research:

```shell
$ dpkg -S /path/to/file
```

# Displaying the Files Installed by a Package
Understanding what is provided in a package is a common need for fixing inter-package incompatibilities:

```shell
$ dpkg -L <package>
```

# Search Packages by Keyword
Looking for a package on any Debian-based system:

```shell
$ dpkg -l <search>
``````
