Tags: #user-configuration #tools #macos 

# Remapping the Keyboard
How to customize [ITerm2](https://iterm2.com/) to behave like a Linux terminal with proper functioning `Alt` and `Ctrl` keys.  Derived from [here](https://www.clairecodes.com/blog/2018-10-15-making-the-alt-key-work-in-iterm2/).

## Left Option is Esc
Remap the left Option key to send `Esc` (really, `Alt`) so that terminal shortcuts like `Alt-b` and `Alt-f` work:

Preferences -> Profiles -> _profile name_ -> Keys -> Left Option key: Esc+

Change for each profile used.

## Left Command is Control
Using one's left pinky to press `Ctrl` is natural, albeit RSI inducing, so it is nice to also map the left command (⌘) to `Ctrl` so one's left thumb can be used.  

**NOTE:** This prevents the left command key from being used to interact with the system forcing the right command key to be used instead.  Since this impacts things like switching windows (⌘-Tab), copy and pasting (⌘-c, ⌘-v), closing a window (⌘-w), etc it should only be used if you're willing to train yourself to use the right command key instead.

# Profile Changes
Setting the scrollback buffer to 1,000 lines:
Preferences -> Profiles -> _profile name_ -> Terminal -> Scrollback lines: 1000