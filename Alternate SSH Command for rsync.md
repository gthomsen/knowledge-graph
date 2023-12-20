Tags: #ssh #utilities 

Specifying an alternate SSH executable for file transfer when using `rsync` is done with the `RSYNC_RSH` environment variable (really, an alternative remote shell in general)

```shell
RSYNC_RSH=/usr/local/bin/ssh rsync -avzh --progress /path/to/transfer/ remote-system:/path/to/transfer/
```

The specification of an alternative remote shell is similar to how [[Alternate SSH Command for Git|Git]] does it.