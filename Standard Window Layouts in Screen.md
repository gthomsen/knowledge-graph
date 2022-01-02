Tags: #screen #utilities #user-configuration 

If one has a standard workflow that always involves setting [[GNU Screen|Screen]] up the same way each time, then the following configuration allows for a simplified setup. The main pieces are:

1.  Creating a `.screenrc` for each workflow
2.  Adding a wrapper shell function for `screen`
3.  Call `screen` slightly differently when creating a new instance

# Individual `.screenrc` Configurations
Each workflow needs to have its `.screenrc` available, assumed to be named `.screenrc-<name>` throughout this example.

Within each configuration, add commands to create named windows, each with a command to run within them. The following starts three windows running 1) Emacs, 2) a shell, and 3) `top`, and then selects the Emacs window to show to the user:

```
screen -t Emacs emacs -nw
screen -t Shell
screen -t Top   top

select 0
```

# Shell Function
A wrapper shell function is needed so that it can intercept invocations and possibly modify the parameters supplied to screen. This simplifies what is required by the end user to start new sessions with each workflow's `.screenrc` configurations.

**NOTE:** We cannot use aliases since we modify the arguments supplied to `screen`.

```shell
# wrap the screen command so that we can pull up different configurations based
# on the task at hand.
function screen()
{
    CONFIG_NAME=$1
    SCREEN_NAME=$2

    SCREEN=`which screen`
    SCREENRC=${HOME}/.screenrc

    if [ -n "${CONFIG_NAME}" ]; then
        SCREENRC="${SCREENRC}-${CONFIG_NAME}"

        # we have a configuration file, specify a name for the screen either
        # using what the user specified or based off of the configuration.
        if [ -n "${SCREEN_NAME}" ]; then
            SCREEN_NAME="-S ${SCREEN_NAME}"
        else
            SCREEN_NAME="-S ${CONFIG_NAME}"
        fi

        # if the configuration requested doesn't exist, simply pass everything
        # provided to Screen itself.  otherwise, run our constructed command.
        if [ ! -f "${SCREENRC}" ]; then
            # this typically handles command line options passed directly
            # to screen like "-ls" or "-dRR".
            COMMAND="${SCREEN} $*"
        else
            # this typically handles creation of new screen instances.
            COMMAND="${SCREEN} -c ${SCREENRC} ${SCREEN_NAME}"
        fi
    fi

    eval ${COMMAND}
}
```

# Invoking `screen`
With the above wrapper shell function, `screen` is now invoked with the following:

```shell
$ screen <name>
```

Where `<name>` is the suffix of a named `.screenrc-<name>` configuration. To name a `screen` session, replace invocations that had `-S <name>` with:

```shell
$ screen <name> <session>
```

This creates a session named `<session>` and can be reattached as normal via:

```shell
$ screen -dRR <session>
```