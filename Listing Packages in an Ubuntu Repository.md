Tags: #utilities #linux #ubuntu 

It does not appear that there is an easy way to enumerate packages provided by a particular repository.  Below is a collection of the least worst options for finding which packages are available - this is particularly useful when a 3rd party provides a repository but the documentation does not list all of the packages necessary (e.g. Intel's oneAPI and the fact that `mpicc` is not part of either the Compiler or MPI packages).

Below are instructions on adding the Intel oneAPI repository and enumerating its packages.

1. Add the repository:
    ```shell
    $ curl -sSL https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS-2023.PUB | sudo apt-key add -
    $ echo "deb [trusted=yes] https://apt.repos.intel.com/oneapi all main " > /etc/apt/sources.list.d/oneAPI.list
    ```
2. Pull an updated list of packages for each repository:
    ```shell
    $ sudo apt-get update
    ```
3. Install `lz4` and parse the packages list:
    ```shell
    $ sudo apt-get install lz4
    $ lz4cat /var/lib/apt/lists/apt.repos.intel.com_oneapi_dists_all_main_binary-amd64_Packages.lz4 | grep ^Package | sort -u
    ```

This [Ask Ubuntu question](https://askubuntu.com/questions/962661/list-all-packages-in-repository) indicates that a clever `curl` command is possible if you know the distribution tag.  

```shell
$ curl -sSL https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS-2023.PUB | sudo apt-key add -

$ awk '{ print $2 $3 }' /etc/apt/sources.list.d/oneAPI.list
https://apt.repos.intel.com/oneapi

$ curl -H 'User-Agent: Debian APT-HTTP/1.3' https://apt.repos.intel.com/oneapi/dists/all/Release
Architectures: all 386 amd64
Codename: all
Components: main
Date: Fri, 11 Feb 2022 19:07:47 +0000
Origin: Intel Corporation
Suite: all
MD5Sum:
 9b4f2a650e37e174feb91daff0d79790 157648 main/binary-all/Packages
 12a0bbed2b11b6f49e87b519936c5290 29310 main/binary-all/Packages.gz
 5ba2d3c7d4982065f65664e146cc1d1f 24507 main/binary-all/Packages.bz2
 30b97c98b05d40f3b0583497d8ee4542 871910 main/binary-amd64/Packages
 6c2a9d7a9ac91491bbfcaf1a039a5510 169965 main/binary-amd64/Packages.gz
 18d314c19cdfaab7aff2fc2f4a90a060 119751 main/binary-amd64/Packages.bz2
 8c8b76939d8a74370e875b9eb4dc9645 414834 main/binary-i386/Packages
 8ad321ca277568a806311afae6362967 70347 main/binary-i386/Packages.gz
 5fa01a1f10fa73419b1da827a5234cfc 56094 main/binary-i386/Packages.bz2
...

$ curl -H 'User-Agent: Debian APT-HTTP/1.3' --stderr - https://apt.repos.intel.com/oneapi/dists/all/main/binary-amd64/Packages | grep ^Package | sort -u
```