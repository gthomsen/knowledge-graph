Tags: #software-engineering #containers #utilities #squid #unfinished

# One-time Setup
Setup and configuration needed before building:
1. [[MITM Caching Proxy with Squid4#Container Image|Build the Squid4 image]]
2. [[MITM Caching Proxy with Squid4#On-Disk Cache|Create a Squid cache]]
3. XXX: Create a certificate authority
4. XXX: Create a trusted MITM certificate

# Start the MITM Caching Proxy
![[MITM Caching Proxy with Squid4#Launching|Launch Squid in MITM mode]]
# Verify the Proxy Works
It is **SIGNIFICANTLY** easier to debug proxy issues on the host than inside the container.  Verify Squid is properly MITM'ing traffic before attempting to build.

```shell
#
# NOTE: we use the system's curl since Conda's version has a strange
#       CA configuration.
#
$ https_proxy=http://localhost:3128 /usr/bin/curl -s https://www.google.com >/dev/null && echo yes
yes
```

If the above does not print `yes` then troubleshoot Squid before proceeding.  This ensures that all issues are only related to the containers and their build.

# Building an Image
Environment variables are handled differently between Docker and Podman so specifying a proxy during a container image build depends on the tool used.

**NOTE:** Watch the Squid log during the build to verify traffic is being handled by Squid rather than passed through.

## Podman
Simply provide the `http_proxy` and `https_proxy` environment variables to the build command to use the caching proxy:
```shell
$ http_proxy=http://localhost:3128 https_proxy=https://localhost:3128 podman build -t image .
```

## Docker
Containers built with Docker earlier than 17.06 require embedding the proxy into the container via environment variables.  All uppercase versions of the environment variables must be used (i.e. `HTTP_PROXY`, `HTTPS_PROXY`, `FTP_PROXY`, and `NO_PROXY`) via the `ENV VARIABLE=VALUE` commands.

Docker 17.07, and newer, can specify proxies via `~/.docker/config.json`:

```shell
$ cat ~/.docker/config.json
{
 "proxies":
 {
   "default":
   {
     "httpProxy": "http://localhost:3128",
     "httpsProxy": "http://localhost:3128",
     "noProxy": "*.test.example.com,.example2.com,127.0.0.0/8"
   }
 }
}
```
```

See the [Docker documentation](https://docs.docker.com/network/proxy/) for details. 