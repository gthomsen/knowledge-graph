Tags: #software-engineering #conda 

**NOTE: This was originally written in July 2021 and may eventually become unnecessary.  As of January 2022, the underlying issue still remains.**

PyQt v5.12.1 is required to [[Building ParaView|build ParaView 5.9.1]] while using Conda.  ParaView has a dependency on Qt and PyQt, though the versions available in the `main` and `conda-forge` channels did not match for the versions required (newer than 5.12).  As a result, PyQt v5.12.1 was built to match the Qt v5.12.1 available in `conda-forge`.  See the available [[#Versions|versions]] to understand the underlying mismatch.

# Building the Conda Package
## Downgrade the `pyqt-feedstock` Version
**NOTE:** The output of this process is available in a fork of the [`pyqt-feedstock`](https://github.com/gthomsen/pyqt-feedstock) repository.  Use it instead of recreating the work.

Clone the `conda-forge` feedstock recipe:
```shell
$ git clone https://github.com/conda-forge/pyqt-feedstock.git
$ git checkout 2c5472a
$ cd pyqt-feedstock
```

Apply the following patch to downgrade the version from v5.12.3 to v5.12.1:
```shell
diff --git a/recipe/meta.yaml b/recipe/meta.yaml
index 2c5472a..d1482d1 100644
--- a/recipe/meta.yaml
+++ b/recipe/meta.yaml

@@ -1,4 +1,4 @@
-{% set version = "5.12.3" %}
+{% set version = "5.12.1" %}

 package:
   name: pyqt_split
@@ -6,13 +6,13 @@ package:

 source:
   - url: https://distfiles.macports.org/py-pyqt5/PyQt5_gpl-{{ version }}.tar.gz
-    sha1: f442a876794947a24474cf85eb02abd60f00f642
+    sha1: 9677d7148ccee1dc7169c1321d3b4e84062d053e

     patches:
       - 0003-configure.patch
       # remove build path from .bat
       - 0004-configure-winbat.patch  # [win]
-      - py2_segfault.diff
-      - qt5_dll.diff
+      #- py2_segfault.diff
+      #- qt5_dll.diff
     folder: pyqt5

   - url: https://distfiles.macports.org/py-sip/sip-4.19.18.tar.gz
```

## Build the Conda Artifacts

Build the package to create `build_artifacts/{channeldata.json,linux-64,noarch}`:
```shell
$ python build-locally.py
```

Create a local Conda channel at `~/local-conda` and copy the package into it:
```shell
$ mkdir ~/local-conda
$ cp -r build_artifacts/channeldata.json build_artifacts/{linux-64/,noarch} ~/code/local-conda/
```

# Installing a Pinned Version
Installation requires pinning the version so that it does not get inadvertently upgraded:

```shell
$ mamba install -c conda-forge --freeze-installed qt 'pyqt==5.12.1' 'pyqt-impl==5.12.1'
```

# Versions
For reference, here are the versions available in the `main` (F) and `conda-forge` (F) channels.

Qt: 5.6.3 (M), 5.9.3 (M), 5.9.4 (M) , 5.9.6 (M), 5.9.7 (M, F), 5.12.1 (F), 5.12.5 (F), 5.12.6 (F)
PyQt: 5.6.0 (M, F), 5.9.2 (M, F), 5.12.3 (F)