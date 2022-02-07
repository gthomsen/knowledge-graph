Tags: #ubuntu #linux #utilities 

# Show Package Metadata
```shell
$ dkpg -s libhdf5-mpi-dev
Package: libhdf5-mpi-dev
Status: install ok installed
Priority: optional
Section: libdevel
Installed-Size: 41
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Architecture: amd64
Source: hdf5
Version: 1.10.4+repack-11ubuntu1
Depends: libhdf5-openmpi-dev, mpi-default-dev
Description: Hierarchical Data Format 5 (HDF5) - development files - default MPI version
 HDF5 is a file format and library for storing scientific data.
 HDF5 was designed and implemented to address the deficiencies of
 HDF4.x. It has a more powerful and flexible data model, supports
 files larger than 2 GB, and supports parallel I/O.
 .
 This package depends on the default MPI version of HDF5 for each platform.
Homepage: http://hdfgroup.org/HDF5/
Original-Maintainer: Debian GIS Project <pkg-grass-devel@lists.alioth.debian.org>
```

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
