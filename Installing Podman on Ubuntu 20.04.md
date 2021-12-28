Tags: #linux #tools #podman #containers

[[Ubuntu]] 20.04 doesn't have Podman installed by default.

Add the OpenSUSE repositories (verify the [signing key](https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/Release.key) before if you feel uncomfortable blindly piping into `apt-key`):
```shell
echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/ /" | sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list

curl -L "https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_20.04/Release.key" | sudo apt-key add -
```

Update the system and install Podman:
```shell
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install podman
```
