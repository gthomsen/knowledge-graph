Tags: #scientific-computing #python #unfinished 

Derived from [Kitware's documentation](https://github.com/Kitware/ParaView/blob/master/Documentation/dev/build.md).

# Dependencies
The following are the direct dependencies:
- Git
- CMake
- Qt5
- Python3
- OpenMPI
- MESA OpenGL

Optional dependencies:
- Intel's Threading Building Blocks (TBB) for multi-core acceleration
- [Ninja](https://ninja-build.org/) to improve the build process
- CUDA for GPU acceleration

# Compilation

## Ubuntu Dependencies

```shell
$ sudo apt install git cmake build-essential libgl1-mesa-dev libxt-dev qt5-default libqt5x11extras5-dev libqt5help5 qttools5-dev qtxmlpatterns5-dev-tools libqt5svg5-dev python3-dev python3-numpy libopenmpi-dev libtbb-dev ninja-build
```

## Conda Dependencies
Build a suitable [[Building PyQt 5.12.1 Conda Package|PyQt]] package and install it.

## Configure and Compile
Make sure the target Python installation exists in the path.  Activate the appropriate Conda environment:
```shell
$ source activate 
```

Source code is available from [Kitware's site](https://www.paraview.org/download/).

```shell
$ wget -O ParaView-v5.9.1.tar.gz 'https://www.paraview.org/paraview-downloads/download.php?submit=Download&version=v5.9&type=source&os=Sources&downloadFile=ParaView-v5.9.1.tar.gz'
$ tar zxf ParaView-v5.9.1.tar.gz
```

Configure ParaView with the following:
- XDMFv3 support - to load HDF5 and netCDF4 datasets
- CUDA support - for GPU acceleration
- Python support - for 
```shell
$ mkdir ParaView-v5.9.1_build
$ cd ParaView-v5.9.1_build
$ cmake \
    -DPARAVIEW_ENABLE_XDMF3=yes \
    -DPARAVIEW_USE_CUDA=yes \
    -DCMAKE_CUDA_ARCHITECTURES=70 \
    -DPARAVIEW_USE_PYTHON=yes \
    -DQt5_DIR=/${CONDA_ROOT}$/lib/cmake/Qt5 \
    -DVTKm_ENABLE_TBB=yes \
    -DVTK_SMP_IMPLEMENTATION_TYPE=TBB \
    -DVTKm_ENABLE_OPENMP=yes \
    -DVTKm_Vectorization=native \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=${HOME}/paraview/5.9.1 \
    ../ParaView-v5.9.1
$ nice -n20 ninja -j16 
```

# Trade Study: Which ParaView Do we Use?
**TL;DR: Build from source so we have control over Python integration**

## Requirements

Needs:
1. Support flexible analysis of large datasets
2. Support label review to understand ML performance

Wants:
1. Programmatic visualization of data

## Prebuilt Package
Pre-built versions are available from Kitware and OS distributor.

ParaView 5.7.1 for Ubuntu 20.04 has a bug that omitted the build environment from the package.  This prevents rebuilding the upstream package against the environment if needed.

### Pros
1. Installation is trivial.  Dependencies are handled automatically (e.g. OpenGL is supported out of the box)
2. Optimized for performance.
### Cons
1. Lags behind the upstream release, especially on LTS distributions
    - Ubuntu 20.04 came out in April 2020 and provided ParaView 5.7.0 from September 2019
    - RHEL is even worse
2. Doesn't have all functionality enabled (e.g. GPU acceleration) or experimental features turned on
3. **Uses the system's Python environment**
    - Limits which packages can be used - OS support greatly lags what is available
    - **Limits what can be done with the Python interface**

## Pre-built Containers
Pre-built containers are available from both [Kitware](https://hub.docker.com/r/kitware/paraview) and [NVIDIA's NGC](https://catalog.ngc.nvidia.com/orgs/nvidia-hpcvis/containers/paraview)

### Pros
1. Recent builds are available
    - NVIDIA has recent builds.  v5.9.0 (January 2021) is the newest version available in January 2022.
    - Continuous integration (CI) builds from Kitware happen regularly.  Monthly?
2. Have the instructions for building the images in the `Dockerfile`'s.
3. Doesn't contaminate the environment
4. **Easily shared with other collaborators**

### Cons
1. Stable builds from Kitware are **OLD**.  v5.7.1 (circa October 2019) is still the newest version available in January 2022.
2. Have to expose GPUs to the container
3. **Uses an unknown Python environment**
    - Limits which packages can be used - OS support greatly lags what is available
    - **Limits what can be done with the Python interface**


## Custom Containers
Assumes [[#Build from Source|building from source]] is a dependency.

### Pros
1. Reproducible builds
2. **Easiest way to share dependencies with collaborators**
3. All of the benefits of [[#Build from Source|building from source]]
### Cons
1. Have to expose GPUs to the container

## Build from Source
Lots of sources for instructions on how to build ([Superbuild with sidecar containers](https://github.com/lhofmann/paraview-superbuild-docker), Ubuntu's package), including the `Dockerfile`'s from [[#Container|containers]].

### Pros
1. Can enable whatever features are necessary.
2. Can stay as bleeding edge as necessary.
3. **Built against a specific installation of Python**
    - Enables use of whatever Python is necessary
### Cons
1. Developer learning curve to build it and its dependencies.
2. Significantly higher troubleshooting cost since no QA has been performed.

# Failed Builds
Historical record for failed builds.  Unless otherwise noted, these occurred on an Ubuntu 20.04 system (GCC 9.3.0).

## 5.10 Development (SHA `83befb5e46`)
Failed due to an incomplete type in VTK-m.

