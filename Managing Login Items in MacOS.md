Tags: #macos 
Things that are launched at login or are running in the background are visible in two ways:
* System Settings > General > Login Items provides a graphical interface to add/remove things launched at login and a way to view background tasks
* `sfltool dumpbtm`  prints status of login and background items

`~/Library/LaunchAgents/` holds plists (others as well?) which may remain even after uninstalling an application by dragging it to the Trash.