Tags: #linux #emacs #screen 

# Who Sets TERM?
The `TERM` environment is responsible for specifying which entry in the termcap database should be used for the current terminal's capabilities.  In principle, no one except the original source terminal should specify the `TERM` environment variable as it prevents the natural propagation of capabilities from client to application that uses said capabilities.  To provide a concrete example of a semi-complex hierarchy of applications that each use `TERM`, consider the following:
- A client terminal application that can run SSH
- The terminal opened when the SSH connection is established
- A GNU Screen session opened within said terminal, with one or more windows each providing a terminal
- Emacs running within a GNU Screen window
- An external sub-shell running within Emacs

If the client is correctly setup, everything down the chain *should just work*.  When in doubt, work to configure the client.

For a quick and dirty hack, the following sections specify how to override `TERM` when you think you know best (you probably don't).  See [[#Enumerating `terminfo` Database]] for acceptable override values.

## Shell
Changing `TERM` in the shell is trivial:
```shell
$ export TERM=xterm-256color
```

## GNU Screen
Changing `TERM` for each spawned Screen window is done via the following configuration:
```
term xterm-256color
```

# Enumerating `terminfo` Database
ncurses provides a table of entries application, `toe`, which reports each of the terminal types supported by curses:

```shell
$ toe | sort | grep ^xterm | head -5
xterm-1002      example of xterm any-button mouse
xterm-1003      example of xterm any-event mouse
xterm-1005      xterm UTF-8 mouse
xterm-1006      xterm SGR-mouse
xterm-16color   xterm with 16 colors like aixterm
```

# Displaying Available Colors

## Shell
`tput` can report the number of colors available based on the `TERM` environment variable's current value:
```shell
$ echo ${TERM}
xterm-256color
$ tput colors
256
```

The following Awk program demonstrates a gradient background with a gray zigzag through it (from this [Emacs Stack Exchange post](https://emacs.stackexchange.com/questions/24784/getting-more-than-8-colors-in-a-terminal-emulator-inside-emacs)):
```shell
$ awk 'BEGIN{
    s="/\\/\\/\\/\\/\\"; s=s s s s s s s s;
    for (colnum = 0; colnum<77; colnum++) {
        r = 255-(colnum*255/76);
        g = (colnum*510/76);
        b = (colnum*255/76);
        if (g>255) g = 510-g;
        printf "\033[48;2;%d;%d;%dm", r,g,b;
        printf "\033[38;2;%d;%d;%dm", 255-r,255-g,255-b;
        printf "%s\033[0m", substr(s,colnum+1,1);
    }
    printf "\n";
}'
```
Terminals that support 24-bit true color produce a gradient output like:
![[resources/terminal-true-color-gradient-good.png]]

While terminals that do not support 24-bit colors produce something... else:
![[resources/terminal-true-color-gradient-bad.png]]

## Displaying Available Colors in Emacs
Emacs can generate a visual display of all of the colors it supports with its details with `M-x list-colors-display`.

# Application Capabilities
## GNU Screen
Supports 8-bit colors just fine with a variety of `TERM` values (`screen.xterm-256colors`, and `xterm-256colors`).

[true color support will come in version 5](https://bbs.archlinux.org/viewtopic.php?id=249670).

## Emacs
Supports 8-bit colors.

Uses 3-bit colors with an unknown value of `TERM`.  `screen.xterm-256color` appears to be unknown in Emacs 27.1.  Manual remapping can be done with the following elisp (derived from this [Stack Overflow post](https://stackoverflow.com/questions/7617458/terminal-emacs-colors-only-work-with-term-xterm-256color)):
```elisp
;; remap GNU Screen's TERM value to something Emacs understands.
(add-to-list 'term-file-aliases
             '("screen.xterm-256color" . "xterm-256color"))
```


