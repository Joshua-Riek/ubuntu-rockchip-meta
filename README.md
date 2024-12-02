# ubuntu-rockchip-meta

This package depends on all of the packages in the Ubuntu Server and Desktop system for Rockchip devices. It's also used to help ensure proper upgrades, so it's recommended to not be removed.

Source code is aviable on GitHub, but packaged on [Launchpad](https://launchpad.net/~jjriek/+archive/ubuntu/rockchip).

## Building

First, you need to set up pbuilder, a tool that creates a clean, minimal environment for the build. This ensures that the build will work everywhere and that it's not dependent on something unusual in your own environment.

Install the following packages on your host system to setup pbuilder:

```bash
# Update package list
sudo apt-get update

# Upgrade packages
sudo apt-get upgrade -y

# Install build dependencies
sudo apt-get install -y pbuilder binfmt-support qemu-user-static qemu-system-arm
```

Building the package is quite easy. Change your working directory to the root of the source tree and type the following commands:

```bash
# Create source package
dpkg-source -b .

# Create base tarball
sudo pbuilder create --architecture arm64 --mirror http://ports.ubuntu.com/ubuntu-ports --distribution "$(dpkg-parsechangelog -S Distribution)"

# Build using the base tarball and source package
sudo pbuilder build --architecture arm64 --mirror http://ports.ubuntu.com/ubuntu-ports --distribution "$(dpkg-parsechangelog -S Distribution)" ../*.dsc 
```
