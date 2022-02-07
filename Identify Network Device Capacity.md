Tags: #linux #utilities #networking

The `/sys/class/net/<device>/speed` file contains a `<device>`'s speed, in Mbps.

```shell
$ cat /sys/class/net/eth0/speed
1000
```

**NOTE:** This file does not exist for virtual devices (e.g. container networking or loopback) nor wireless devices.

Systems that have `lshw` installed can get fancier output, with the `size:` and `capacity:` lines being of interest:

```shell
$ lshw -class network
WARNING: you should run this program as super-user.
  *-network
       description: Ethernet interface
       product: RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller
       vendor: Realtek Semiconductor Co., Ltd.
       physical id: 0
       bus info: pci@0000:04:00.0
       logical name: enp4s0
       version: 16
       serial: aa:bb:cc:dd:ee:ff
       size: 1Gbit/s
       capacity: 1Gbit/s
       width: 64 bits
       clock: 33MHz
       capabilities: bus_master cap_list ethernet physical tp mii 10bt 10bt-fd 100bt 100bt-fd 1000bt-fd autonegotiation
       configuration: autonegotiation=on broadcast=yes driver=r8169 duplex=full firmware=rtl8168h-2_0.0.2 02/26/15 ip=192.168.1.1 latency=0 link=yes multicast=yes port=MII speed=1Gbit/s
       resources: irq:36 ioport:f000(size=256) memory:fd504000-fd504fff memory:fd500000-fd503fff
WARNING: output may be incomplete or inaccurate, you should run this program as super-user.
```