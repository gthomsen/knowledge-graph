Tags: #screen #utilities 

GNU Screen can nest windows so that other Screen sessions are running inside of a parent Screen session's window.  While this exponentially increases the mental load to understand which window you're working with (now you also need to track sessions) it does enable more advanced use cases, such as debugging a multi-process application which has one window per debugger per process, all inside a single window of the parent session.

Here is an example that creates the following hierarchy of Screen windows:
1. Nested session #1 (`nested-1`) on current host:
    1. Emacs
    2. Terminal
2. `top` running on current host
3. Nested session #2 (`nested-2`) running on a system called `dev`:
    1. Emacs
    2. Terminal
    3. `top` running on `dev`

```shell
# create a new session on the host and attach it.
(host) $ screen -S current-host

# create a detached session and then attach it.
(host) (0) $ screen -dmS nested-1
(host) (0) $ screen -r nested-1

# rename the nested session's first window to "Emacs".
(host) (nested-1) (0) $ C-a a A Emacs RET

# create a new window in the nested session and name it "Terminal".
(host) (nested-1) (Emacs) $ C-a a c
(host) (nested-1) (1) $ C-a a A Terminal RET

# create a new window in the host session and run top.
(host) (nested-1) (Terminal) $ C-a c
(host) (1) C-a c

# log into the dev system and start a new session.
(host) (2) $ ssh dev
(host) (2) (dev) $ screen -S nested-2

# create a window in the remote sesion for Emacs.
(host) (2) (dev) (nested-2) $ C-a a A Emacs - remote RET
(host) (2) (dev) (nested-2) (Emacs - remote) $ C-a a c
(host) (2) (dev) (nested-2) (1) $ C-a a A Terminal - remote RET
(host) (2) (dev) (nested-2) (Terminal - remote) $ C-a a c
(host) (2) (dev) (nested-2) (2) $ C-a a A top - remote
(host) (2) (dev) (nested-2) (top - remote) $

# detach the remote session and log out.
(host) (2) (dev) (nested-2) (top - remote) $ C-a a d
(host) (2) (dev) $ exit
(host) (2) $

# detach the host's session.
(host) (2) $ C-a d
(host) $
```

As sessions are nested, the prefix key is repeated (once per nesting) to interact with the nested session.  Using just the prefix key itself interacts with the parent session.