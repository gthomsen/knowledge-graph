Tags: #utilities #linux #macos 

Setting a terminal's X11 window title can be accomplished with the following escape sequence:
```
echo -ne "\033]0;SOME TITLE HERE\007"
```

Note that the above sequence will be interpreted by terminal multiplexers as well (e.g. `screen`) so it matters whether you set a title and then enter a session or set the title from within the session.  For `screen` the former will update the Screen window's title and not the X11 window, while the later will affect the X11 window.