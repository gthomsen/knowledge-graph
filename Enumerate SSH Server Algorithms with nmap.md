Tags: #ssh #utilities 

Occasionally it is useful to know which algorithms a SSH server offers (e.g. configuring a server-specific configuration in `${HOME}/.ssh/config`) and `nmap` lets you do that without having access to the server's configuration, or reading through a SSH connection's debug logs:
```shell
$ nmap --script ssh2-enum-algos -sV -p 22 192.168.1.1
Starting Nmap 7.80 ( https://nmap.org ) at 2024-01-04 07:46 EST
Nmap scan report for system.local (192.168.1.1)
Host is up (0.00022s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh2-enum-algos:
|   kex_algorithms: (6)
|       curve25519-sha256
|       curve25519-sha256@libssh.org
|       diffie-hellman-group-exchange-sha256
|       diffie-hellman-group14-sha256
|       diffie-hellman-group14-sha1
|       kex-strict-s-v00@openssh.com
|   server_host_key_algorithms: (3)
|       rsa-sha2-512
|       rsa-sha2-256
|       ssh-ed25519
|   encryption_algorithms: (5)
|       chacha20-poly1305@openssh.com
|       aes128-gcm@openssh.com
|       aes256-gcm@openssh.com
|       aes128-ctr
|       aes256-ctr
|   mac_algorithms: (3)
|       hmac-sha2-512-etm@openssh.com
|       hmac-sha2-256-etm@openssh.com
|       umac-128-etm@openssh.com
|   compression_algorithms: (2)
|       none
|_      zlib@openssh.com
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.18 seconds
```

Algorithms for key exchange (`kex`), host keys, the stream's encryption, its message authentication (`mac`), and compression are listed in server priority order.  Clients can connect using any combination of the algorithms offered by the server.