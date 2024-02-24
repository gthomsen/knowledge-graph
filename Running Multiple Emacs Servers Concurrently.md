Tags: #emacs 

Starting an Emacs server process allows `emacsclient` to quickly connect to an existing Emacs session and edit files in it.  Each server has a name which means that multiple can run concurrently.  If one does set unique names for each, Emacs will complain with the following:

```
 stop  Warning (server): Unable to start the Emacs server.
There is an existing Emacs server, named "server"
To start the server in this Emacs process, stop the existing server or call `M-x server-force-delete' to forcibly disconnect it.
```

Servers can be named through the `EMACS_SERVER` environment variable when it starts:
```shell
(shell1) $ EMACS_SERVER=server_name emacs ...
```

One can also set `server-name` in an existing Emacs session:
```
M-: (setq server-name "server_name")
M-x server-start
```

Connecting to a specific server with `emacsclient` is done as follows:
```shell
$ emacsclient -s server_name
```