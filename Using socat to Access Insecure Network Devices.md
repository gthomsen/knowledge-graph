Tags: #linux #macos #utilities #openssl 

SSL3 is laughably insecure and has been removed from modern browsers.  Unfortunately this prevents access to older systems (e.g. DD-WRT, orphaned IoT devices, etc) that may still be chugging along.  

# Building socat
Download and unpack the [latest version](https://www.dest-unreach.org/socat/download/socat-1.7.4.1.tar.bz2): 
```shell
$ wget https://www.dest-unreach.org/socat/download/socat-1.7.4.1.tar.bz2
$ tar jxf socat-1.7.4.1.tar.gz
```

Confirm that the version of OpenSSL you're building against supports the versions of SSL/TLS of interest ![[OpenSSL Quirks#Listing Supported Ciphers]]
Build against a specific version of OpenSSL.  This version is baked into `socat` so you don't have to do any environment manipulation at run-time.
```shell
$ cd socat-1.7.4.1
$ ./configure --enable-openssl-base=/path/to/openssl
```

# Changing TLS/SSL Versions Through MITM

Breakdown of the example below:
1. The local server's (the MITM) certificate and key (`CERT=...`, along with the ciphers it will support (`SSLSRV=...`)
2. The client cipher when accessing the target server (`SSLCLI=...`)
3. Running the local server on `127.0.0.1:11443` 
4. Connecting to the target server on `192.168.1.123:443`
```shell
# set environment variables so we can understand the core structure
# in the socat command below.
$ CERT="cert=cert.pem,key=key.pem" SSLSRV="cipher=AES256-SHA,method=TLS1.2,verify=0" SSLCLI="cipher=AES128-SHA,method=SSL3,verify=0"
$ socat OPENSSL-LISTEN:11443,bind=127.0.0.1,reuseaddr,fork,${CERT},${SSLSRV} OPENSSL:192.168.1.123:443,${SSLCLI}
```