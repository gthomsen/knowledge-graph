Tags: #containers #X11 #ubuntu 

Buffered terminal access within containers is problematic - either it hangs, doesn't echo the readline inputs without a forced refresh, or just does something weird.  Setting up a VNC server inside the container and exposing it to the host sidesteps that by using X11 for keyboard input.  A sledgehammer to kill a mosquito but in this case the mosquito is invisible thanks to a dearth of search keywords that lead to a solution.

The sections below install a VNC server, a basic window manager, and a terminal.  When the server is launched and its port exposed to the host, external VNC clients can connect to the server.

# Package Installation
The below `Dockerfile` fragment updates the APT package list and installs Tight VNCServer, the Motif Window Manager, some X11 fonts, and a simple X11 terminal (`xterm`).

```shell
RUN \
    apt update && \
    apt-get install -y --no-install-recommends \
                       mwm \
                       tightvncserver \
                       xterm \
                       xfonts-base xfonts-75dpi xfonts-100dpi \
                       && \
    rm -rf /var/lib/apt/lists/*
```

Note that explicitly installing the `xfonts-*` packages is required since the installation uses `--no-install-recommends` which prevents them from being transitively installed.

# VNC Server Configuration
The following creates a VNC-specific X11 startup script (`${HOME}/.vnc/xstartup`) and sets a password to access the VNC session (`${VNC_SERVER_PASSWORD}`).
```shell
RUN \
    mkdir -p ${HOME}/.vnc && \
    /bin/echo -e '#!/bin/sh\nmwm &\nxterm &\n' > ${HOME}/.vnc/xstartup && \
    chmod +x ${HOME}/.vnc/xstartup && \
    echo "${VNC_SERVER_PASSWORD}" | vncpasswd -f > ${HOME}/.vnc/passwd && \
    chmod 600 ${HOME}/.vnc/passwd
```

# Launching the VNC Server
A VNC server can either be launched interactively (e.g. from within `podman run --rm -it image`) or spawned as part of the `ENTRYPOINT` (or `CMD`) commands.  Regardless of how, the following is a reasonable starting point for the command:

```shell
# creates a VNC server on X11 display :1 with a resolution of 1600x1200.
$ vncserver -geometry 1600x1200 :1
```

# Exposing the VNC Server on the Host
With the VNC server running on X11 display `:N`, it listens for incoming client connections on port `5900 + N`.  For example, VNC server on display `:10` will open port `5910`.  Expose this to the host when launching the container, like so:

```shell
CONTAINER_VNC_PORT=5910
HOST_VNC_PORT=5910
$ podman run --rm -it -p ${CONTAINER_VNC_PORT}:${HOST_VNC_PORT} image
```

Change `${CONTAINER_VNC_PORT}` based on the display chosen.  Change `${HOST_VNC_PORT}` based on the ports available on the host.  Note that these do not have to match.