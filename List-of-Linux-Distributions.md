# List of Linux Distributions that I like
# First, what is a Linux Distribution?
Every Linux system has the Linux [Kernel](/What-is-the-Kernel-anyway.md) at it's center, with a suite of other programs helping it keep track of what resources are available, and what programs are running.

Anyone with an idea that they think is good, and enough time to pursue it, can make choices about how the system should be configured, what hardware will be supported, and what programs should be included alongside the Kernel.  Additionally, such a person would also have to make choices about which configuration choices will be left to the user. After those choices are made, that person could make a package for *distribution*.

Once the Linux System is installed, it is in the hands of the root user and all of that can be changed, but it is often helpful to have default settings that make sense. As you explore, you may find that the default settings of some distributions appeal to your preferences more than others.

In this guide I'll discuss some of the most common distributions that I've worked with in terms of:
- How complicated they are to install, configure, and operate.
- What degree of choices are made by default vs choices left to the user during installation.
- The complexity and usefulness of the package manager.
- Nuances you might want to be aware.


# Ubuntu
Available at: https://ubuntu.com/download/server

### Complexity: Easy
The installation process of both the desktop and server versions of Ubuntu feature helpful text boxes where you'll need to enter some information, such as the username and password for the first user you'd like to create.  The installer presents a few options about disk and file system configuration, with sane defaults selected, accompanied by warnings about potential data loss. Those warnings make a lot more sense if you are not installing Ubuntu on a machine with a fresh blank hard drive or a new virtual instance -- as most users will be.

Ubuntu uses the `apt` package manager, which is configured by default to use official repositories maintained by Ubuntu.  The repositories feature most popular software, so the process of installing a new package is often as simple as running:
```
sudo apt install package-name
```

Even the desktop version of Ubuntu features a graphical front end for the pacakge manager with search functionality.

# Debian
Available at: https://www.debian.org/distrib/

### Complexity: Medium
Debian will feel strangely familiar for users who began with Ubuntu.  This is because Ubuntu is derived from Debian, but significantly different enough to be it's own distribution.

Most of the differences between Ubuntu and Debian stem from the philosophical differences by the makers of those pieces of software. Ubuntu provides a great number of very useful programs that are no cost to the user, but have restricive licensing agreements. Debian uses a much more strict definition of the word *free* which means, "I can do whatever I want with it" and does not provide non-free software by default.

As such, it is possible to perform an installation of Debian where the core tools are installed, but the *apt* package manager is configured only to scan the installation media for packages instead of Debians offical repository or any of it's mirrors -- and even then you may have to reconfigure your package manager to scan for non-free software.

The official Debian package repository and it's mirrors also include a less extensive selection of packages.  Some software projects such as Chromium or Mysql even go so far as to configure their own Debian repositories which feature only the software made by the project.  Users may then configure that repository in the *apt* package manager and scan it for updates and upgrade normally as they would with core system utilities.

# CentOS
Available at: https://www.centos.org/centos-linux/

### Complexity: Medium
CentOS is the open source distribution of RedHat linux -- which you may recognize as a major player in Linux for commercial use.  The open source licensing of linux obligates the makers of RedHat to release their source code freely so that others may build on it, and they do so under a different label/brand as CentOS.

The installation process involves a graphical menu that is somewhat more difficult to navigate.

CentOS uses the *yum* package manager.  Because CentOS is the same as RedHat and both are designed for enterprise use, the official repositories which the package manager downloads software from do feature most of the popular programs that you might need.

There is a difference we should note here.  In Ubuntu and Debian, when you install a service that listens for incoming connections like Apache, or Mysql, the package manager will download the software and place it in a standard location, and then also start the service and *enable* the service so that it starts automatically after the server is rebooted.  If you install services using *yum* on CentOS, the package manager will download the necesary software packages and place them in a standardized location on the server, but the user must then start enable the services separately.