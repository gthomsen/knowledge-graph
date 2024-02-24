Tags: #X11 #tools 

A VNC server's resolution is specified when it is started, though this resolution may need to change over its lifetime. This can occur when running the VNC viewer on different systems or even the same system with different monitors attached (e.g. laptop-only vs laptop with external 24" display).

Use `xrandr` to change resolution for a given X11 session. The current resolution (marked with an asterisk) and a list of available resolutions is returned when run without arguments:

```shell
$ xrandr
Screen 0: minimum 32 x 32, current 1920 x 1080, maximum 32768 x 32768
VNC-0 connected 1920x1080+0+0 0mm x 0mm
   1024x1205     60.00 +
   1920x1200     60.00
   1920x1080     60.00*
   1600x1200     60.00
   1680x1050     60.00
   1400x1050     60.00
   1360x768      60.00
   1280x1024     60.00
   1280x960      60.00
   1280x800      60.00
   1280x720      60.00
   1024x768      60.00
   800x600       60.00
   640x480       60.00
```

Changing resolution can be done via `xrandr -s <width>x<height>`:

```shell
$ xrandr -s 1600x1200
```

VNC will always present a single screen, though `xrandr` can change specific screens' resolutions via the `--output <screen> --mode <width>x<height>`. The following is equivalent to `xrandr -s 1600x1200` in a VNC session:

```shell
$ xrandr --output VNC-0 --mode 1600x1200
```
