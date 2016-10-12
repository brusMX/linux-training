# Install the MEAN Stack

Now that we are inside our machine we need to install these tools:

1. MongoDB
1. Node.js
1. Bower and Gulp
1. MEAN

## Package managers (.deb and .rpm)

There are many out in the wild but these are some of the most popular ones. The first one is the high-level package manager that provides a simple way to retrieve and install packages including dependency resolution and multiple sources. Then we have the low-level package manager that can only install, remove, provide info and build packages. The con is that it does not automatically download and install the package dependencies.

1. **YUM -> RPM** - Red Hat Enterprise Linux (RHEL), CentOS, Scientific Linux, Fedora, etc.
1. **Advanced Packaging Tool (APT-GET) * -> DPKG** - Ubuntu, Debian, KNOPPIX, etc.(Debian based distros)
1. **ZYPPER -> RPM** - Open SUSE, SUSE Linux Enterprise Server

### $ sudo yum install

First of all lets get the latest definitions:

```Shell
sudo yum update
```

