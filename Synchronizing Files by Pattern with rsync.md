Topics: #utilities 

`rsync` can transfer just a subset of files that match one or more patterns instead of a full directory tree, but requires multiple whitelist (`--include <pattern>`) and blacklist options (`--exclude <pattern>`) to achieve.

The following synchronizes just paths ending in `.config` from the local system to a remote:
```shell
$ rsync -avz --include "*/" --include "*.config" --exclude "*" /path/to/directory remote_host:/path/to/remote/directory
```