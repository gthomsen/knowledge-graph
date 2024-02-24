Tags: #ssh #utilities 

Specifying an alternate SSH executable for file transfer when using `rsync` is done with the `RSYNC_RSH` environment variable (really, an alternative remote shell in general)

```shell
RSYNC_RSH=/usr/local/bin/ssh rsync -avzh --progress /path/to/transfer/ remote-system:/path/to/transfer/
```

The above specification of an alternative remote shell is similar to how [[Alternate SSH Command for Git|Git]] does it.  The `--rsh <cmd>` (or `-e <cmd>`) option may be used if specifying an environment variable is not possible.  The command above looks like the following with a command line option:
```shell
$ rsync -avzh --progress -e /usr/local/bin/ssh /path/to/transfer/ remote-system:/path/to/transfer/
```