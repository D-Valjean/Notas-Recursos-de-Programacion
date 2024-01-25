# Downloading and Installing

October 2, 2017 · 3 min · Jamie Cameron | [Suggest Changes](https://github.com/webmin/webmin.com/tree/master/content/download.md)

## Repository

### Setup

The simplest and best way to get [**Webmin**](https://webmin.com/about/) is to use automatic [**`setup-repos.sh`**](https://github.com/webmin/webmin/blob/master/setup-repos.sh) script to configure repositories on your **RHEL** or **Debian** derivative systems. It can be done in two easy steps:

```
curl -o setup-repos.sh https://raw.githubusercontent.com/webmin/webmin/master/setup-repos.sh
sh setup-repos.sh
```

This script will automatically setup our repository and install our GPG keys on your system, and provide **`webmin`** package for installation and easy upgrades in the future. The supported and tested systems are **Red Hat Enterprise Linux**, **Alma**, **Rocky**, **Oracle**, **CentOS Stream**, **Fedora** or **Debian**, **Ubuntu**, **Kali**.

### Install

If Webmin repository was setup using our **`setup-repos.sh`** as [described above](https://webmin.com/download/#setup) then Webmin can be installed as easy as:

#### RHEL and derivatives

```
dnf install webmin
```

#### Debian and derivatives

```
apt-get install webmin --install-recommends
```

### Access

After successful Webmin installation, you can access its interface by entering **`https://<Your-Server-IP>:10000`** in your browser. Check that your firewall configuration allows access through port **10000**.

## Manual

The latest full Webmin distribution is available in various package formats for download:

[**`rpm`**](https://www.webmin.com/download/rpm/webmin-current.rpm) — **Red Hat Enterprise Linux**, **Alma**, **Rocky**, **Oracle**, **CentOS Stream**, **Fedora**, **openSUSE**

[**`deb`**](https://www.webmin.com/download/deb/webmin-current.deb) — **Debian derivatives (Ubuntu, Kali, Parrot, Pop!, Lite, Devuan)**

[**`pkg`**](https://www.webmin.com/download/solaris-pkg/webmin-current.pkg.gz) — **Solaris**

[**`tar`**](https://www.webmin.com/download/webmin-current.tar.gz) — **FreeBSD** or any other Linux distribution

  * The minimal [**`tar`**](https://www.webmin.com/download/webmin-current-minimal.tar.gz) version of Webmin contains only the core API and programs, and a few modules required for its basic operation. Most modules and all themes have been left out, but can be easily added later. It can be useful if you only need some of the programs functionality, and don’t want to download the entire multi-megabyte package.

### Checksum Verification

To verify that you have downloaded Webmin fully and correctly, you can use the command **`sha256sum`** on the downloaded file, and compare it against those listed below:

|File|SHA256 Checksum|
|---|---|
|webmin_2.105_all.deb|d257060d92409e2ec68856b484a8333044ef08000bdc5c66705d7f55407931d9|
|webmin-2.105-minimal.tar.gz|306bc44caf8afdc57743301121d7bec7f6cd8cbfd907d7e1d5eac864b1ecd477|
|webmin-2.105-1.noarch.rpm|d85a74a0d17f4c5701318d77b9d7afb94884c962f87db233fd2366b455d87181|
|webmin-2.105-1.src.rpm|e6b6a193762af54a3ff913cb8495318b26c095047462e2eef955673dff15c39e|
|webmin-2.105.pkg.gz|f91e0be42beadb74764401fbc587225a9820c7712315734cecc78d0ce9c635a0|
|webmin-2.105.tar.gz|3693fe7560469d1bfd2d175b329ba16996974e0285f7be889bdb750877c4e5d5|
|webmin-2.105.zip|3ba83269851603ce828a3c1d876537a6cdfd342b972595fc0c33da6ed076a608|

### Configure

If Webmin package was downloaded manually it can be installed:

#### RHEL and derivatives

```
dnf install ./webmin-current.rpm
```

#### Debian and derivatives

```
apt-get install --install-recommends ./webmin-current.deb
```

#### Solaris

```
# The root user be switched from a role account to a normal account to logins to work
rolemod -K type=normal root
# Uncompress
gunzip webmin-current.pkg.gz
# Install
pkgadd -d webmin-current.pkg
```

#### FreeBSD and any other Linux installation from source

```
# Change directory
cd /tmp
# Uncompress
gunzip webmin-current.tar.gz
tar xf webmin-current.tar.gz
cd webmin-current
# Install
./setup.sh /usr/local/webmin
```

If you installed it by specifying an installation directory parameter to **`setup.sh`** as the instructions above show, i.e. **`/usr/local/webmin`**, the original **`webmin-current`** directory can now be safely deleted.

The source package can be installed on any of the supported OS, such as **FreeBSD**, **macOS**, **HP/UX**, **AIX**, and all other flavors of Linux. However, if your system supports one of the other package formats like **`rpm`** or **`deb`** packages, it is _recommended_ to install it from that type of package.

## Older Versions

Older versions of Webmin can be downloaded from [Sourceforge](https://sourceforge.net/projects/webadmin/files/webmin/).

## Standard Modules

The standard modules that you may have deleted from Webmin on your system can be re-installed by downloading using [this](https://download.webmin.com/download/modules/) link.

## Development Builds

There are development pre-release and nightly builds available for testing purposes only. These builds may be unstable or lack certain features. Use them at your own risk!

### Pre-release Builds

Pre-release builds can be found on [devel.webmin.com](https://download.webmin.com/devel/) page.

### Nightly Builds

Nightly builds can be found on [builds.webmin.dev](https://builds.webmin.dev/) page.

[](https://webmin.com/download/#top)

© 1997 - 2024 [Webmin](https://webmin.com/about/#developers)