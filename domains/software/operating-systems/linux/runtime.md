---
layout: default
title: Linux Runtime
parent: Linux Kernel
nav_order: 1
---

# Linux kernel runtime
{: .no_toc }

## Kernel configuration
To check the configuration of a running linux based OS:
- `zcat /proc/config.gz | grep <desired-config>`
- [link](https://unix.stackexchange.com/questions/511983/where-is-config-hz-defined)

## Modprobe

### Auto-load a kernel module
- create a config file file named as the kernel module in the `/etc/modules-load.d/` folder
- place the kernel module inside the `/lib/modules/$(uname -r)` folder (can be a sub-folder)
- optional: create a config file named as the kernel module in the `/etc/modprobe.d/`
    - can add soft dependencies
    - can modify the install instructions
        - caution: the default one (insmod) won't be executed
- run `depmod -a`


