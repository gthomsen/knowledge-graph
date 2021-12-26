Tags: #linux 

# `xterm`
Newer Ubuntu systems have `xterm` sending the `Meta` key whenever the `Alt` modifier is pressed.  This results in things like `ä` whenever `Alt-f` or `Alt-b` are pressed.

```shell
$ echo 'XTerm*metaSendsEscape: true' >> ~/.Xresources
```
Either restart the X11 server or merge the Xresources database via [[Xresource Database - xrdb]].
