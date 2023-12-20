Tags: #shell-scripting #software-engineering 

Reading lines of data into a variable in a `while` loop is easy enough to make work in simple conditions, but is surprisingly fraught with sharp edges once the loop body does non-trivial work or needs to modify variables outside of the loop.  Consider the following:

```shell
GLOBAL_COUNTER=0
echo "one\n\two\three" | while read LINE
do
    ./do_stuff.sh
    GLOBAL_COUNTER=$((GLOBAL_COUNTER + 1))
done
echo ${GLOBAL_COUNTER}
```

Ignoring the fact that one can pass a string into the loop via a *here string* (cousin of the *here document*), the above code prints out `0` instead of `3`.  This is because the `echo ... | while read LINE`  invokes a pipeline which causes the loop body to execute in a subshell, rather than inside the original shell, which means modifications to `GLOBAL_COUNTER` are not made in the parent process.

*Here strings* solve the above problem and results in the following:
```shell
GLOBAL_COUNTER=0
INPUT_DATA="one\n\two\three"
while read LINE
do
    ./do_stuff.sh
    GLOBAL_COUNTER=$((GLOBAL_COUNTER + 1))
done <<<"${INPUT_DATA}"
echo ${GLOBAL_COUNTER}
```

The above addresses the subshell problem, but it still suffers from shared standard input across the lines executed in the loop body.  As a result, the loop trip count may be 1, 2 or 3 depending on what `./do_stuff.sh`  does with standard input.  To address that problem, one needs to separate the loop's `read` command's input from the shell's standard input, which is inherited by default for each command executed in the body.  This is done with the `-r <descriptor>` option in `read` and specifying a file descriptor in the *here string* use, like so:

```shell
GLOBAL_COUNTER=0
INPUT_DATA="one\n\two\three"
while read -r 99 LINE
do
    ./do_stuff.sh
    GLOBAL_COUNTER=$((GLOBAL_COUNTER + 1))
done 99<<<"${INPUT_DATA}"
echo ${GLOBAL_COUNTER}
```

The above will always report `3`, regardless of whether `./do_stuff.sh` reads from standard input or not.

***NOTE:*** If the `echo ...`  above represents a non-trivial command to execute, one can achieve the same as using *here strings* by opening a file descriptor redirecting it into the loop.  How that is done is an exercise for the reader.
