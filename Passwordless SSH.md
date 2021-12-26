Tags: #ssh #unfinished 

# Create a Key Pair
# Configure Key Forwarding
# Distribute Public Keys
# Authenticate with Local Agent
# Login

# XXX: Merge
#1 Public/Private Key Pair Creation:  
  
On your laptop, run:  
  
$ ssh-keygen -b 384 -t ecdsa -f ~/.ssh/nidia-laptop  
<enter passphrase twice>  
  
The passphrase will be required in step #4 each time.  Don't leave it  
empty.  Pick something secure since this is now your "password" when  
logging in via password-less SSH.  
  
#2 Forward Your Private Key  
  
You'll need to forward your keys on the Cornell workstations so you  
can ssh from your laptop to Prometheus to Fania, all without a  
password.  Note that forwarding exposes your key to privileged users  
on the remote system so you'll only want to do it on select systems  
rather than as a default option (you shouldn't trust systems by  
default).  
  
To do so, add the following into ~/.ssh/config  (replace the <values>  
as appropriate):  
  
Host prometheus  
   HostName     <IP address>  
   User              <username>  
   ForwardAgent  yes  
  
Host fania  
   HostName     <IP address or name>  
   User              <username>  
   ForwardAgent yes  
  
Note that the names after "Host" don't have to be resolvable by DNS -  
these are aliases that you can set to whatever you want.  
  
Make sure the config has permissions 0600:  
  
$ chmod 0600 ~/.ssh/config  
  
#3 Distribute Public Key  
  
You need to copy the contents of ~/.ssh/nidia-laptop.pub into  
~/.ssh/authorized_keys on both Prometheus and Fania.  If you've never  
setup ~/.ssh/authorized_keys, you can simply do this from your laptop:  
  
# assumes step #2 above is done.  you'll type your password for each of these.  
$ scp ~/.ssh/nidia-laptop.pub prometheus:~/.ssh/authorized_keys  
$ scp ~/.ssh/nidia-laptop.pub fania:~/.ssh/authorized_keys  
  
If you have setup ~/.ssh/authorized_keys before, then just copy the  
contents of yourlaptop:~/.ssh/nidia-laptop.pub to the end of  
remotehost:~/ssh/authorized_keys.  Be careful about word wrapping -  
each key should take up one line in authorized_keys.  
  
Make sure that remotehost:~/.ssh/authorized_keys has permissions 0600:  
  
$ ssh prometheus chmod 0600 ~/.ssh/authorized_keys  
$ ssh fania chmod 0600 ~/.ssh/authorized_keys  
  
#4 Authenticate your Key  
  
For each terminal, you'll now need to run the following:  
  
$ `eval ssh-agent`; ssh-add ~/.ssh/nidia-laptop  
<passphrase>  
  
At this point, you can log into either Prometheus or Fania without a  
password from this terminal.  Closing the terminal will force you to  
open a new one and rerun the above (technically not true, but a  
convenient lie).  You may have a key manager application via your  
desktop environment that prompts you for a phassphrase when you login  
though that is Gnome or KDE specific - search for "gnome ssh key  
agent" and you should get where you need to be.  
  
#5 Passwordless Login  
  
You can now SSH to Prometheus or Fania without a password prompt.  You  
should also be able to SSH to the other one without a password as  
well.  
  
If you can't log into the first system, then review #2 and #3.  If you  
can't log into the second system from the first then review #2 and  
verify you get output like so when you run on your laptop and the  
first system:  
  
$ ssh-add -l  
2048 SHA256:FUsb56UMIY+o4ca9/8KGLMw9A7CTW84QnVoYOuGjg4A  
/home/user/.ssh/id_rsa (RSA)  
  
Note that the line printed will look different due to the paths and  
key type (RSA 2048-bit vs ECDSA 384-bit), though you're looking for  
output or not.
