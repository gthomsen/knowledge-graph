Tags: #linux #debugging #software-engineering #fortran 

Debugging symbols are often useful when debugging and profiling code that wanders into a system library so there is more context than the following:
```
==112438== Conditional jump or move depends on uninitialised value(s)
==112438==    at 0x521181F: ??? (in /usr/lib/x86_64-linux-gnu/libgfortran.so.4.0.0)
==112438==    by 0x5214D2F: ??? (in /usr/lib/x86_64-linux-gnu/libgfortran.so.4.0.0)
==112438==    by 0x520A5FE: ??? (in /usr/lib/x86_64-linux-gnu/libgfortran.so.4.0.0)
==112438==    by 0x520A6DC: ??? (in /usr/lib/x86_64-linux-gnu/libgfortran.so.4.0.0)
==112438==    by 0x10F619: some_user_function_ (user_code.f90:229)
```

Without debugging symbols it isn't always clear what exactly the issue is with `some_user_function()` at `user_code.f90:229`.  Once they're installed, it is clear that an uninitialized value was passed to a Fortran `write()` statement:

```
==114199== Conditional jump or move depends on uninitialised value(s)
==114199==    at 0x521181F: get_float_string (write_float.def:1070)
==114199==    by 0x5214D2F: _gfortrani_write_real_g0 (write.c:1760)
==114199==    by 0x520A5FE: formatted_transfer_scalar_write (transfer.c:2063)
==114199==    by 0x520A6DC: formatted_transfer (transfer.c:2279)
==114199==    by 0x10F619: some_user_function_ (user_code.f90:229)
```

Debian provides debugging packages for each release, though they need to be added to the APT source list beneath `/etc/apt/sources.list.d/`:

```shell
$ echo "deb http://ddebs.ubuntu.com $(lsb_release -cs) main restricted universe multiverse
deb http://ddebs.ubuntu.com $(lsb_release -cs)-updates main restricted universe multiverse
deb http://ddebs.ubuntu.com $(lsb_release -cs)-proposed main restricted universe multiverse" | sudo tee -a /etc/apt/sources.list.d/ddebs.list
```

Debugging packages have their own signing key that needs to be imported before the package list can be refreshed:

```shell
$ sudo apt install ubuntu-dbgsym-keyring
$ sudo apt update
```

`find-dbgsym-packages` maps files to debugging packages and is provided by the `debian-goodies` package:

```shell
$ sudo apt install debian-goodies
```

Identifying packages can be done like so:

```shell
$ find-dbgsym-packages /usr/lib/x86_64-linux-gnu/libgfortran.so.4.0.0
libgfortran4-dbg
```

Though it is more likely that you don't care which package provides it, but rather to install the missing package.

```shell
$ sudo apt install `find-dbgsym-packages /usr/lib/x86_64-linux-gnu/libgfortran.so.4.0.0`
```

Derived from [here](https://wiki.ubuntu.com/Debug%20Symbol%20Packages).