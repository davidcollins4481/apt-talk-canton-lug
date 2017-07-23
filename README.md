# All About APT

A talk about APT for Canton Linux User Group. [Resources] ()

## What is "APT"

APT stands for *Advanced Packaging Tool*. One of several different package management
tools for UNIX-based systems. Update, install, or remove software packages. Other similar tools are RPM (Redhat), Pacman (Arch)

## Brief History of APT

A lot of the details about the history have been lost. Original development mostly done on IRC. Introduced in 1998. The first Debian version that included it was Debian 2.1, released on 9 March 1999.

## What is a "package"?

This could be the topic of another talk. Each package manager has it's own format for packages. The most generic definition: **a compressed file archive that contains all of the files for a particular application**.

APT uses Debian packages which end in a .deb file extension. Packages can be distributed an installed by themselves similar to Windows MSIs or Mac OS DMG files. A .deb package file is not installed via APT, however. To install a standalone package you must use another package manager called **dpkg**. So what is the difference between dpkg and APT?

## De-tangling the confusing mess of terms

There are quite a few tools that can be used to install packages in Debian-based distros. Here's an attempt to clarify some of the differences

**dpkg** - a low-level tool meant to just install, get information, or configure a specific package archive. There is a some functionality built in to query installed packages and get details on installed packages. No dependency management and will not interface with remote repository sources like APT.

**APT** - a package manager with included tools (apt-get, apt-cache, apt-key, etc). APT is a high-level tool that manages dependencies, 

**aptitude** - an nCurses-based front-end to dpkg. Basically a friendlier interface to dpkg

**synaptic** - a GTK-based (graphical) front-end to APT. A user-friendly interface for APT 


## Basic Commands

Many users will be able to run the following commands and not need to know much else:

(see apt-get man page for more details)

**Synchronize package index with remote sources in `/etc/apt/sources.list`**

`sudo apt-get update`

`sudo apt-get upgrade`

`sudo apt-get dist-upgrade`

`sudo apt-get install <package-name>`

`apt-cache search <query>`


## upgrade vs dist-upgrade
* If a new version of a package needs a new dependency, `apt-get dist-upgrade` will upgrade and install the dependency, `apt-get upgrade` won't.

* If a new version of a package conflicts with an already installed package, `apt-get dist-upgrade` may remove the conflicting package and upgrade the other, `apt-get upgrade` won't.

* `apt-get update` will NEVER remove or install a new package. If a package update requires a new package the update will be held back by `apt-get update`


## Searching for Packages

### Search Repos
use `apt-cache search` 

### Search for packages already installed
there are several ways to do this. 

`dpkg -l | grep <package name>`
`apt list --installed` (In Ubuntu 14.04 and above)


## Diving Deeper into a package

### Package details
Use `apt-cache show` to get details about a package in the repositories

You can use `dpkg -s <packagename>` to get the status of a package

### Find what package a file belongs to
`dpkg -S <filename>`


### Exploring /etc/apt/sources.list

## Anatomy of a repo source line
`deb http://us.archive.ubuntu.com/ubuntu/ yakkety main restricted`

`deb` - Archive type. This can be `deb` of `deb-src`. `deb` sources contain binary packages. `deb-src` sources contain source code packages

`http://us.archive.ubuntu.com/ubuntu/` - URL to retrieve the packages from

`yakkety` - distribution name. In this case "yakkety" is a release code name for the Ubuntu release. But this can be the release code name OR the release class. Ubuntu doesn't really use release class names like Debian does. Examples for Debian ("stable", "testing", "unstable")




# Housekeeping

`apt-get autoremove` - Apt handles dependencies for you when installing a package. But sometimes, dependencies change. If a package you have installed no longer requires a dependency it once did `apt-get autoremove` will remove it. It will NEVER remove a package you installed via `apt-get install`. If there is a package you want to keep that was installed as a dependency you can `apt-mark` it as being installed manually.


## Resources

APT Github Repository [[https://github.com/Debian/apt](https://github.com/Debian/apt)]

APT Debian Documentation [[https://www.debian.org/doc/user-manuals#apt-howto](https://www.debian.org/doc/user-manuals#apt-howto)]

APT History [[https://en.wikipedia.org/wiki/APT_(Debian)#History](https://en.wikipedia.org/wiki/APT_\(Debian\)#History)]

dpkg [[https://en.wikipedia.org/wiki/Dpkg](https://en.wikipedia.org/wiki/Dpkg)]

Sources List [[https://wiki.debian.org/SourcesList](https://wiki.debian.org/SourcesList)]
