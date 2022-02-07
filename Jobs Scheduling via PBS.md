Tags: #cheatsheet 

**NOTE:** The commands below have been tested on PBS Professional.

# Queue Investigation
Find queues with particular attributes.  Queues without the target attribute simply have their name listed:
```shell
$ qstat -Q -f | egrep -e '(^Queue|gpu)'
```