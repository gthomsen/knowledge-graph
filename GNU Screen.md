Tags: #linux #utilities #emacs 

***NOTE:*** Everything below assumes a custom prefix key of `j` instead of `a`.

# Custom Prefix Key
`Ctrl-a` is a regularly used shortcut to go to the beginning of a line and conflicts with screen's default prefix key.

Add `escape ^Jj` into `~/.screenrc` to remap it to `Ctrl-j`.

# Flow Control
When flow control is disabled, `Ctrl-s` cannot be sent to the system which prevents Emacs from searching (`C-s`) or saving (`C-x C-s`).

Toggle flow control via `C-j f`.  Alternatively, `C-j : flow off` if one can't remember the keybinding.

GNU screen's [manual on the topic](https://web.mit.edu/gnu/doc/html/screen_14.html).

# Splitting Windows
Screen's view can be split into multiple regions so multiple windows.

Creating vertical regions side-by-side (`C-j |`) or horizontal regions on top of each other (`C-j S`).

Removing the current region (`C-j X`).  Removing _all_ regions at once (`C-j Q`).

Switching between regions (`C-j TAB`).  Finer grained movement can be done via command mode (`C-j : <command>`) where the following commands are available:
- `up`, `down`, `left`, `right`
- `next`, `prev` (relative to creation order)

Regions can be resized via the command mode:
- `resize +N`  - Increase the region by `N` rows/columns
- `resize -N` - Decrease the region by `N` rows/columns
- `resize N` - Set the region to `N` rows/columns

Region layouts can be saved (`layout dump /path/to/layout.dump`) and restored (`source /path/to/layout.dump`) via command mode.
