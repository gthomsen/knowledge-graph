Tags: #software-engineering #openssl #service #docker #squid #unfinished

Full image builds are painful when repositories aren't mirrored locally, even with a fast internet connection.  Setting up Squid to cache build content requires a MITM proxy with an custom certificate authority and a self-signed certificate.  Once this is in place

**NOTE: I have not been able to get the Squid4 image to build on ARM64 so this is Linux-specific for the time being.**

This was derived from [[Network Proxy Gymnastics|various articles]].

# Dependencies

## Container Image
Clone and build the Squid4 Docker image contained in [this repository](https://github.com/gthomsen/docker-squid4):

```shell
$ git clone https://github.com/gthomsen/docker-squid4.git
$ cd docker-squid4
```

Build the container image with Podman:
```shell
# compile Squid with 16 processes.
$ podman build --build-arg CONCURRENCY=16 -t docker-squid4 .
```

## On-Disk Cache
Squid will cache everything it can on disk, up to the limits specified in its configuration file (unknown default).  Be sure to locate the cache on a partition with enough space.

Create a cache for use:
```shell
$ mkdir -p ${HOME}/squid/cache
```

## Trusted Certificate
XXX: Create a certificate authority and a trusted certificate

# Launching 
**WARNING: The below assumes the MITM certificate authority is trusted by the system.  This is a security vulnerability as an attacker could issue additional certificates that are implicitly trusted by the system.**

Launch the proxy in MITM mode on `localhost:3128`:
```shell
$ podman run -it --rm 
    -p 127.0.0.1:3128:3128 \
    -v /home/gthomsen/squid/cache/:/var/cache/squid4/ \
    -v /etc/ssl/certs/:/etc/ssl/certs/:ro \
    -v /etc/ssl/private/squid-mitm.key:/squid-mitm.key:ro \
    -v /etc/ssl/certs/squid-mitm.crt:/squid-mitm.crt:ro \
    -e MITM_CERT=/squid-mitm.crt \
    -e MITM_KEY=/squid-mitm.key \
    -e MITM_PROXY=yes \
    docker-squid4
```

Highlights of the above:
- Maps the host's certificate store into the containers (`-v /etc/ssl/certs/:/etc/ssl/certs/:ro`) so the Squid instance's certificate is trusted.
- Maps the Squid instance's certificates and key into the instance (`-v /etc/ssl/private/squid-mitm.key:/squid-mitm.key:ro -v /etc/ssl/certs/squid-mitm.crt:/squid-mitm.crt:ro`).
- MITM Configuration for Squid4 (`-e MITM_CERT=/squid-mitm.crt -e MITM_KEY=/squid-mitm.key -e MITM_PROXY=yes`).
