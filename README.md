Linux kernel
============

There are several guides for kernel developers and users. These guides can
be rendered in a number of formats, like HTML and PDF. Please read
Documentation/admin-guide/README.rst first.

In order to build the documentation, use ``make htmldocs`` or
``make pdfdocs``.  The formatted documentation can also be read online at:

    https://www.kernel.org/doc/html/latest/

There are various text files in the Documentation/ subdirectory,
several of them using the reStructuredText markup notation.

Please read the Documentation/process/changes.rst file, as it contains the
requirements for building and running the kernel, and information about
the problems which may result by upgrading your kernel.

Prepare environment
=================

    sudo update && sudo upgrade -y && sudo apt install build-essential fakeroot wget bzip2 bc python bison flex rsync libelf-dev libssl-dev xz-utils libncurses-dev dwarves git debhelper ncurses-dev -y

Build
=====

    make clean
    sudo cp -rf /boot/config-$(uname -r) .
    sudo chown $USER:$USER config-$(uname -r)
    mv config-$(uname -r) .config
    make menuconfig
    scripts/config --disable SYSTEM_TRUSTED_KEYS
    scripts/config --disable SYSTEM_REVOCATION_KEYS
    make bindeb-pkg -j `nproc` LOCALVERSION=-ryzen9

Install
=======

    cd ..
    sudo dpkg -i *.deb
    reboot

Check
=====

    uname -mrs

Tested
======

My workstation:
![image](https://github.com/user-attachments/assets/2bf3d446-0242-4845-bd70-8fe85b8cb344)

