Tags: #macos #paraview #user-configuration

Intel x86-64 ParaView can run through Rosetta2 emulation though requires additional environment variables:
```shell
$ export VTK_DISABLE_VISRTX=1
$ export VTK_DISABLE_OSPRAY=1
$ /Applications/ParaView-5.9.0.app/Contents/MacOS/paraview
```

Add `VTK_DISABLE_VISRTX` and `VTK_DISABLE_OSPRAY` into your user configuration and logout/login to be able to run ParaView from Finder.