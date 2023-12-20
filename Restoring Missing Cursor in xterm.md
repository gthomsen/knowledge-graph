Tags: #linux #utilities 

Sometimes applications that manage the terminal via `curses` do not reset things back to "normal" and, as a result, cause the cursor to disappear.  The following resets things (even when `reset` does not):

```shell
$ tput cnorm
```

Derived from [this answer on Stack Exchange](https://unix.stackexchange.com/a/512630).