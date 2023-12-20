Tags: #linux #macos 

# Arrays
Arrays can be indexed either by numeric values (from zero) or by arbitrary strings (as an associative array/hash map).  These are only supported in Bash 4.x and newer, which limits their use on MacOS' stock Bash which is frozen in time at 3.2.57 (as of 2022/12/07 on 13.0.1).

Declaring arrays is done via the `declare` command and requires choosing whether an array or an associative array is needed:
```shell
# ARRAY is indexed by integer values, starting at 0.
declare -a ARRAY

# ASSOCIATIVE_ARRAY is indexed by strings.
declare -A ASSOCIATIVE_ARRAY
```

# Declaring Variables
Declaring variables prior to their first use is done via the `declare` command.

If a variable is defined in a function it will have local scope unless specified with a global scope via `-g`:
```shell
function do_something()
{
    # this is only accessible within do_something().
    declare LOCAL_VARIABLE

    # this will be accessible once do_something() returns.
    declare -g GLOBAL_VARIABLE
}
```