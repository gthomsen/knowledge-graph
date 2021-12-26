Tags: #scientific-computing 

Simple script that launches a command and prints the memory used while it is running.

Areas to customize:
1. Change the command run (`sleep 100` below)
2. Change the memory metrics measured (`pmem`, `rss`, and `vsz` below)

```shell
#/bin/sh  
  
sleep 100 &  
COMMAND_PID=$!  
  
# check that the command launched is still running.  
#  
# NOTE: this does not actually send a signal to the target process.  
#  
while kill -0 "${COMMAND_PID}" >/dev/null 2>&1; do  
    NOW=`date +%s`  
  
    MEMORY_MEASUREMENTS=`ps -u ${USER} -o pmem,rss,vsz  | grep -v "RSS" | xargs`  
  
    # report the time and the current memory usage.  this outputs three columns  
    # per process found by ps (note that it could be refined to search for  
    # specific processes) along with the time so it is easy to plot in another  
    # tool (Excel, Matlab, etc).  
    #  
    # NOTE: redirect this to a log file for retention.  
    #  
    echo ${NOW} ${MEMORY_MEASUREMENTS}  
  
    sleep 60  
done
```