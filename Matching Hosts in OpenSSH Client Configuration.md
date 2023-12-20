Tags: #ssh 

OpenSSH configuration file parsing constructs its configuration with a "first match wins" policy.  This means that care is required in ordering configuration directives so host-specific directives occur before defaults.  Unfortunately, for configurations working with a large number of disparate systems there may not exist a clever sequence of directives that works for every system.  For these, conditional application of directives is required which is what the `Match` directive provides.

Once a `Match` directive is encountered, it is applied to all of the following directives up until the next `Host` or `Match`.

The syntax of the `Match` directive is not obvious from  `ssh_config(5)` (and it appears to have changed over time) but allows one or more, whitespace separated parameters which specify how the conditional is performed.  Hosts are matched via the `host="<hostname_or_pattern>"` parameter.  The `all` parameter can be used in lieu of `host="*"`.

Providing configuration to all hosts in the `example.com` domain:

```conf
Match canonical host="*.example.com"
    # configuration applicable only to *.example.com hosts goes here.

Match canonical all
    # default configuration goes here.
```

Derived from [Damien Miller's blog](http://blog.djm.net.au/2014/01/hostname-canonicalisation-in-openssh.html) (canonicalization) and several Stack Exchange posts ([demonstrates concepts with old syntax](https://unix.stackexchange.com/questions/741771/in-ssh-config-what-does-match-canonical-all-mean), [new syntax that works with OpenSSH 9.3](https://unix.stackexchange.com/questions/562486/ssh-config-how-to-have-match-match-multiple-hostnames-in-one-line)) posts.