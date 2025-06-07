---
layout: default
title: Linux Drivers Best Practices 
parent: Linux Drivers
nav_order: 1
---

# Best practices in device driver development
{: .no_toc }

## Device mapping
<!-- TODO: describe how to map the device internals to C code structures -->
- use device version specific header files to specify enumerations for register addresses
- use device version specific source files to specify data structures to hold important information
    - register reserved bits from datasheet
    - register default values from datasheet
    - define linux kernel-specific or user defined structure to best fit the need

## Device interaction interface
<!-- describe how to wrap the device mapping so that the implementation specifics are hidden -->
- hide the device mapping details
- expose functions that are related with interacting with the device
- expose read and write functions
- expose bulk read and write functions
    - be vary careful with this because of error handling  and reverting to old state when error occurs
    - use with protocols that are able to handle bulk transactions and have a known mechanism to revert
- expose read and write functions that have specific behaviour depending on what you are reading and writing
    - if only some cases need other register to be read or written
    - i.e. port selection, unlocking/locking, ...
    - if all registers need additional operations then include that in regular read write and don't expose
    specific functions

## Device description
<!-- describe how to describe how the device is connected -->
TODO:

### Device hardware configuration description
<!-- touch on OF (devicetree) configuration and best practices -->
<!-- mention ACPI -->
TODO:

## Device configuration
<!-- approaches on how to configure the device -->
TODO:

### Default device configuration
TODO:

### Pre-compile device configuration
TODO:

### Runtime device configuration
TODO:

## Exposing driver attributes to sysfs
- device attribute helper functions and macros are defined in
[`<linux/device.h>`](https://github.com/torvalds/linux/blob/master/include/linux/device.h)

### Registering device attributes
- create device attribute structure using the pre-compile macro
`DEVICE_ATTR(name, mode, show, store)`
- additional macros for specific way to create device attributes exist:
    - `DEVICE_ATTR_RW(_name);`
        - creates attribute `_name` with RW permissions and
        `_name_store` and `_name_show` functions
    - `DEVICE_ATTR_RO(_name);`
        - creates attribute `_name` with RO permissions and
        `_name_show` function
    - etc.
- to create the sysfs files for attributes call the following function
after the `device_register` function call cal:
`device_create_file`

## Links and resources
- [Driver porting: Devices and attributes](https://lwn.net/Articles/31220/)
- [How to Create a sysfs File Correctly](https://www.linuxfoundation.org/blog/how-to-create-a-sysfs-file-correctly/)
- [User space kernel space interaction](https://pothos.github.io/papers/linux_userspace_kernel_interaction.pdf)


