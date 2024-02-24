Tags: #ssh #utilities 

To show the SHA256 fingerprint of a public SSH key, regardless of its type, use the following:
```shell
$ ssh-keygen -l -v -f /path/to/key.pub
2048 SHA256:4N8aYG3LZcqGlSWqwAMPYmmngIKoGf0avUwJWIcQOOA key (RSA)
+---[RSA 2048]----+
|*o...            |
|B+o.             |
|%Eo.  . . .      |
|BBo+ o + +       |
|o.* = = S o      |
|   B + O *       |
|  . + . O .      |
|       . o       |
|        .        |
+----[SHA256]-----+
```

This shows both the fingerprint (`2048 SHA256:... key (RSA)`) as well as the visual fingerprint.