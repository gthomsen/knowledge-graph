Tags: #linux 

The system's Xresources (`/etc/X11/Xresources/*`) and user's Xresources (`~/.Xresources`) are read whenever the X11 server starts.  Resources can be modified while running via `xrdb`.

# Updating the Xresources Database
Merging new resources onto existing, where new resources overwrite old:

```shell
$ xrdb -merge ~/.Xresources
```