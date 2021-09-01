# Build instructions for rpi

To build on a raspberry-pi, you'll have to hack around the docker issues that plague their latest distribution.

This boils down to two things:
- Upgrade docker
- Fix a libseccomp issue

## Docker upgrade
Full instructions are at https://docs.docker.com/engine/install/debian/, but here's the gist.
```
$ sudo apt-get remove docker docker-engine docker.io containerd runc
$ sudo apt-get update
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
$ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
$ echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## libseccomp fix
You'll need to upgrade libseccomp as well.  This requires getting the latest version from sid.

- download the armhf binary from https://packages.debian.org/sid/libseccomp2
- `sudo dpkg -i <binary_you_downloaded_above>

