Tags: #linux #utilities 

Installation:
```shell
$ sudo apt install cgroup-tools
```

Create a group called `cgroup_name` that limits both memory and CPU utilization.  `user` can modify the resource restrictions and launch processes in the group:
```shell
$ sudo cgcreate -t user:user -a user -g memory,cpu:cgroup_name
(user) $ cgset -r memory.limit_in_bytes=$((1024*1024*1024*1)) group_name
(user) $ cgexec -g memory,cpu:group_name ls
```

**NOTE:** Unclear if there is a better approach to setup a control group's limits as `root`  but allow `user` to launch processes.