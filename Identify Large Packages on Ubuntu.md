Tags: #ubuntu #linux #utilities 

`dpigs` is part of the `debian-goodies` package.  Sizes are pre-computed during package installation so the report generation is immediate.

List 20 largest packages with human-readable sizes:
```shell
$ sudo apt install debian-goodies
$ dpigs -n 20 -H
 579.6M linux-firmware
 323.0M libgl1-mesa-dri
 312.7M libgl1-mesa-dri
 267.2M libnvidia-gl-460
 257.9M openjdk-9-jre-headless
 217.5M firefox
 214.7M golang-1.13-go
 195.6M sagemath-common
 192.9M linux-modules-extra-5.4.0-91-generic
 192.8M linux-modules-extra-5.4.0-90-generic
 192.7M linux-modules-extra-5.4.0-80-generic
 183.7M docker.io
 174.9M libvtk7.1p
 163.0M openjdk-11-jre-headless
 157.2M paraview
 155.6M linux-image-extra-4.13.0-31-generic
 143.4M containerd
 131.8M libboost1.71-dev
 127.4M snapd
 116.4M nodejs
```