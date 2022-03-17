Tags: #linux 

The below is useful when dealing with IoT devices/appliances that come with a default IP address that lives on a different network than your own.  Adding a route enables direct communication to the device (within reasonable assumptions about the networking infrastructure).

Route for an entire network:
```shell
$ sudo route add -net 192.168.1.0/24 enp4s0
```

Route for an individual system:
```shell
$ sudo route add -host 192.168.1.1 enp4s0
```