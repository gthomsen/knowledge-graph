Tags: #shell-scripting #software-engineering 

Command line processing of options needs to be particularly robust otherwise a shell script's behavior depends on the order of options supplied.  Assuming the `-o BAD` option below generates an unhandled error, the following command lines are parsed differently.

```
# Four non-option arguments: "-t one two three"
$ ./test-empty-array.sh -o BAD -t one two three

# Three non-option arguments: "one two three"
$ ./test-empty-array.sh -t -o BAD one two three
```

In this case, `test-empty-array.sh` contains the following code:
```shell
# process a command line option
#
# NOTE: this is a Bash function (due to the associative array) but is used to highlight
#       a non-obvious error.
#
process_option()
{
    ARGUMENT="$1"

    declare -gA ARRAY

    # do stuff with ${ARGUMENT}.

    #
    # NOTE: Bash produces a warning about indexing an associative array with
    #       an empty string, but actually generates an error which exits this
    #       function on the next line.
    #
    ARRAY[""]="value"

    # these lines will not be executed.
    echo "This isn't printed"
    /bin/true
}

# state controlled by the '-t' option that indicates whether it was handled or not.
FLAG="no"

# parse known options and their arguments.  getopts() returns a failure if the last
# command executed failed.
while getopts "o:t" FLAGS
do
    case ${FLAGS} in
        o)
            process_option "${OPTARG}"
            echo "This won't be printed either"
            ;;
        t)
            FLAG="yes"
            ;;
    esac

    echo "Hello from flag '${FLAGS}'"
done

# compute the number of command line arguments processed as options and remove them
# from the command line.
NUMBER_OPTIONS=`expr ${OPTIND} - 1`
shift ${NUMBER_OPTIONS}

# report the state after execution.  the bug from above becomes apparent when
# the script verifies the number of arguments and receives one additional
# depending on the order of '-t' and '-o' on the command line.
echo "Number of arguments: $#"
echo "Number of option arguments: ${NUMBER_OPTIONS}"
echo "Flag: ${FLAG}"
```

Even with more than two decades of non-trivial shell scripting experience, the above code was surprising when the following line executes:
```shell
ARRAY[""]="value"
test-empty-option.sh: line 19: ARRAY[""]: bad array subscript
```

On the surface, it appears that Bash has identified a problem and issued a warning though in reality it generated an error and kicked off a cascade of early returns that are ultimately hidden by `getopts()`'s silent error handling.  The following facts each contribute to the two command lines at the top resulting in different argument lists:

1. Shell builtins that error cause the calling function to stop executing.  This is different than if an external command fails.
2. `case` statements stop executing when they encounter an error
3. `getopts()` stops processing options when it encounters an error
4. `getopts()` has silent option processing by default

As a result the options `-o BAD -t` only processes the `-o BAD` portion of the command line, while `-t -o BAD` processes both options.  Because of this, `getopts()` increments `OPTIND` a different number of times for each which prevents consistent validation of the number of remaining command line arguments.

While trying to untangle the above mess, one additional fun fact was learned - loops have an exit status that can be queried, where the status is the status of the last command executed.  All of the subtleties and cascading errors could have been immediately identified if `$?` was checked after the `getopts()` loop.