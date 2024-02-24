Tags: #emacs 

`emacsclient` can be used to quickly [[Running Multiple Emacs Servers Concurrently|edit files in an existing session]] though exiting it can be a challenge.  Consider editing `file1` like so:

```shell
$ emacsclient file1
```

The normal shortcut to quit Emacs will quit the server process (which is almost never what you intend) so one must use `C-x #` to run `server-edit`.  While this doesn't strictly quit, it marks a file that `emacsclient` was invoked on as completed and, at the end of the file list, `emacsclient` exits.

If one invokes `emacsclient` without specifying a file, the `server-edit` function does not quit `emacsclient` as in the above.  Instead, one must use `C-x 5 0` to run `delete-frame`.