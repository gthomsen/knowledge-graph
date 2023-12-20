Tags: #linux #utilities #ssh #kerberos

Linux session keyrings hold secrets that can be accessed by processes for a given session (typically logging in at a graphical prompt, or via SSH) and provide the framework for securely handling said secrets.  Since this works in the background, most people are unaware of it's existence which makes for fun when troubleshooting tooling that relies on it.

In particular, Kerberos relies on the session keyrings to manage its tickets.  Should one find interacting with a Kerberos tool providing an error message like the following:

```shell
$ klist
Key has been revoked while resolving ccache
```

One can confirm that there is no session keyring present with:
```shell
$ keyctl show @s
Keyring

Unable to dump key: Key has been revoked
```

A new session needs to be created so Kerberos can access it:

```shell
$ keyctl session
$ keyctl show @s
Keyring
 889917837 --alswrv   1000  1000  keyring: _ses

# this is the expected output when no Kerberos tickets are held.
$ klist
klist: No credentials cache found (filename: /tmp/krb5cc_1000)
```

# GNU Screen and Sessions
Losing a session is a frequent occurrence when using GNU Screen due to how session keyrings are created and destroyed.  In particular, keyrings are created when a user logs in (e.g. while sitting at a workstation, or via SSH) but are also destroyed when the user logs out (e.g. closing the SSH connection).  Even though processes inherit keyrings from their parent, destroying said keyring will cause long-lived processes to encounter the error above.

Derived from [`session-keyring(7)`](https://www.man7.org/linux/man-pages/man7/session-keyring.7.html).