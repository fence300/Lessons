# Setting up a practice environment on Windows

### Preparing the host machine
- Install virtualbox on the windows host (if not already installed)
- Install PuTTY on the windows host (if not already installed)
- Install PuTTYgen on the windows host (if not already installed)

# Decide on a Linux Distribution
For more detail about each item in this list, check out my [List of Linux Distributions](/List-of-Linux-Distributions.md)
- For beginners, I highly recommend starting with Ubuntu.
- Once you have some familiarity with Ubuntu, Debian might be a good next-step.
- After Debian, try out CentOS.

# Obtain a Linux installation image:
- download the .iso file from a reliable source
- optional: verify the package by comparing the hash/checksum with the one published by the makers


# Create the new virtual machine in Virtual Box where you will install linux
- Check the minimum and recommended system specs for your distribution
    - VirtualBox defaults to like 8g hard drive/storage space, but most distributions usually wants more if you're installing apps on it
    - VirtualBox defaults to 1G but most distributions are hungry for at least 2G.
- After the virtual machine is "created" go into settings for that machine and set
    - Networking -> Bridged interface
    - Storage -> Disk Drive -> select the .iso file


# "Start" the virtual machine and follow the directions given by the installer
- Most of the time, the Linux installer will ask you how you want to partition the disk.  Because you have created a virtual machine for this purpose, you can ignore any warnings about overwriting existing data.
- Creating partitions to separate each big component of the file system like `/home`, `/tmp`, and `/boot` may make sense for some applications, but those are beyond the scope of this guide.
- Some installers may require a network connection to download additional packages from the internet. In fact,some installers try to be small enough to fit on a traditional CD, so they contain only a minimal installer and must download nearly everything from the internet.
- Every installer I have ever worked with at some point asks to set the system clock to the local timezone.
- At some point, you must provide the credentials you'll use to login to the new system.
    - Sometimes that's just setting the root password
    - Some installers will ask you for the username and password of an initial user.  That user will have administrative privilege to execute commands as root via `sudo`