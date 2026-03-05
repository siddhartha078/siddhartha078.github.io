---
title: "Linux From Scratch"
excerpt: "Built a fully functional Linux system entirely from source code, gaining a deep understanding of the Linux ecosystem."
header:
  image: /assets/images/LFS.png
sidebar:
  - title: "Built With"
    text: "GCC Toolchain, Bash, Linux Kernel"
  - title: "Features"
    text: "Extremely flexible, completely customizable, built from the ground up."
---

LFS is like the skeleton of a house, but it's up to us to install plumbing, electrical outlets, kitchen, bath, wallpaper, etc. We have the ability to turn it into whatever type of system we need it to be, customized completely for ourselfs.

### How I built it

The process starts by using a host Linux system to compile a **temporary cross-compilation toolchain**(a private set of compilers and utilities isolated from the host, ensuring the new system is entirely self-contained).

Once that environment was ready, I chrooted into the new partition and compiled every essential package from scratch — **from the shell to the core system libraries**. This included manually configuring the **Linux Kernel**, hand-picking drivers for my specific hardware, and installing a bootloader to bring the whole handcrafted system to life.


> #### Benefits of making an LFS
-  LFS teaches people how a Linux system works internally.
-  Building LFS produces a very compact Linux system.  
-  LFS is extremely flexible, completely customizable.
-  LFS offers you added security as we will compile the entire system from source, thus allowing us to audit everything


> #### What I've Learnt
-  How the components of a Linux system fit and depend on each other.
-  How a cross-compilation toolchain works and why it matters.
-  How to configure and build a custom Linux kernel.
-  How the boot process works, from bootloader to init.
-  How to customize it to my own tastes and needs.



### Credits

Official site: [Linux From Scratch](https://www.linuxfromscratch.org/lfs/)
Reference when troubleshooting: [LFS 12.4 - How to build Linux From Scratch 12.4 - Youtube](https://www.youtube.com/playlist?list=PLyc5xVO2uDsBaLsOXqFX-1sKpkqQaSH22)

