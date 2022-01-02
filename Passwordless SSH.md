Tags: #ssh #user-configuration 

Overview of how to securely access remote systems without having to type your password in repeatedly.  This becomes the foundation for more complex tunneling and connections with SSH.

At a high level, the following is necessary to login without a password:
1. Create a key pair
2. Distribute your public key to each remote system
3. (Optional) Configure your system to forward your keys
4. Locally authenticate your key
5. Log into remote system

Steps #1 through #3 are setup and steps #4 and #5 happen once(ish) per remote connection.

# Create a Key Pair
Create a secure key pair with a strong passphrase.  This is typically done once, though you can setup one key per server to limit the damage if it is ever stolen.

The passphrase chosen here replaces your password as the secret you enter before logging in remotely.  Once created, the passphrase is the only thing that protects the private key should it be exposed in an unauthorized manner.  

**NOTE:** The passphrase entered here never expires.

```shell
$ ssh-keygen -b 384 -t ecdsa -f ~/.ssh/key
... enter passphrase ...
... confirm passphrase ...
```

The above creates a 384-bit elliptic curve key pair in `~/.ssh/key` (private key) and `~/.ssh/key.pub` (public key).  The private key should never be shared, while the public key can be distributed to anyone without reducing your security.

The key type (`-t`) and bit depth (`-d`) can changed as necessary. 

# Distribute Public Keys
You need to copy the contents of `~/.ssh/key.pub` into  
`~/.ssh/authorized_keys` on the remote system once per key pair.  If you've never  
setup `~/.ssh/authorized_keys` on the remote, you can simply copy your public key over (replace `remotehost` as appropriate):  

```shell
$ scp ~/.ssh/key.pub remotehost:~/.ssh/authorized_keys  
```
  
If you have setup `~/.ssh/authorized_keys` before, then just copy the  
contents of `~/.ssh/key.pub` to the end of  
`remotehost:~/ssh/authorized_keys`.  Be careful about word wrapping -  
each key should take up one line in `authorized_keys`.  
  
Make sure that `remotehost:~/.ssh/authorized_keys` has permissions `0600`:  

```shell
$ ssh remotehost chmod 0600 ~/.ssh/authorized_keys
```
  
# (Optional) Configure Key Forwarding
**NOTE:** This section is optional and can be skipped if you will not need to connect to a 2nd remote system from the first (e.g. pushing to or pulling from a remote Git repository).  

Only configure this for remote systems that you trust.  Do not blindly add this into your SSH configuration.

Forwarding the SSH agent to untrusted systems exposes your private key to anyone who has privileges.  Alternatively, you can skip this section and connect via `ssh -A` to selectively forward the SSH agent as necessary.
  
Add the following into `~/.ssh/config`  (replace the `<values>`  as appropriate):  

```
Host remote
   HostName      <IP address>
   User          <username>
   ForwardAgent  yes
```
  
Note that the names after `Host` don't have to be resolvable by DNS -  these are aliases that you can set to whatever you want.  
  
Make sure the config has permissions `0600`:  

```shell
$ chmod 0600 ~/.ssh/config  
```
  

# Authenticate with Local Agent
For each terminal, you'll now need to run the following:  

```shell
$ `eval ssh-agent`; ssh-add ~/.ssh/key
... enter your passphrase ...
```
  
At this point, you can log into the remote system without a password.  Closing the terminal forces you to  open a new one and rerun the above (technically not true, but a  
convenient lie).  Some desktop environments (e.g. GNOME, KDE, or MacOS's KeyChain)  may have a key manager application that acts as the SSH agent and prompts you a phassphrase when you login.

# Login  
You can now SSH to `remotehost` without a password prompt.  Logins from `remotehost` to other hosts can be done password-less by either [[#Optional Configure Key Forwarding|forwarding the agent]] or repeating the entire process above on `remotehost` - forwarding the agent is strongly recommended.