# Debugging Linux kernel

## Inspecting memory dumps

Utilize the `slub_debug=FPZU` in the `cmdline` boot loader parameter. This functionality doesn't require special debug kernel configuration.
This will enable the kernel to use an exception like handler when memory corruptions happen within the kernel and print out an elaborate report of what happened.
Example output:
```
[    3.081314] =============================================================================
[    3.089490] BUG kmalloc-128 (Not tainted): Object already free
[    3.095317] -----------------------------------------------------------------------------
[    3.095317]
[    3.104987] INFO: Allocated in ds90ub948_of_to_reg_config+0x284/0x690 age=6 cpu=4 pid=107
[    3.113165] INFO: Freed in ds90ub948_of_to_reg_config+0x544/0x690 age=6 cpu=4 pid=107
[    3.121001] INFO: Slab 0x00000000d6136822 objects=21 used=6 fp=0x00000000625bf16f flags=0x1ffff00000010201
[    3.130650] INFO: Object 0x00000000625bf16f @offset=6656 fp=0x0000000000000000
[    3.130650]
[    3.139349] Redzone  00000000006831ab: bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb  ................
[    3.148825] Redzone  000000003d92170e: bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb  ................
[    3.158302] Redzone  000000005d4feb92: bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb  ................
[    3.167780] Redzone  000000002258aad9: bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb  ................
[    3.177258] Redzone  000000002f64e21b: bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb  ................
[    3.186736] Redzone  00000000fdf3fe15: bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb  ................
[    3.196214] Redzone  000000002b8aa319: bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb  ................
[    3.205692] Redzone  000000004369b88b: bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb bb  ................
[    3.215171] Object   00000000625bf16f: 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b  kkkkkkkkkkkkkkkk
[    3.224649] Object   00000000c3cd5e27: 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b  kkkkkkkkkkkkkkkk
[    3.234127] Object   000000003b8662c7: 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b  kkkkkkkkkkkkkkkk
[    3.243605] Object   000000000a338bf2: 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b  kkkkkkkkkkkkkkkk
[    3.253083] Object   000000008bb40e00: 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b  kkkkkkkkkkkkkkkk
[    3.262561] Object   00000000b9f8e5d7: 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b  kkkkkkkkkkkkkkkk
[    3.272039] Object   00000000af911847: 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b  kkkkkkkkkkkkkkkk
[    3.281517] Object   000000003fe059b8: 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b 6b a5  kkkkkkkkkkkkkkk.
[    3.290995] Redzone  00000000a47eb339: bb bb bb bb bb bb bb bb                          ........
[    3.299778] Padding  00000000178729c1: 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a  ZZZZZZZZZZZZZZZZ
[    3.309256] Padding  00000000e33976b5: 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a  ZZZZZZZZZZZZZZZZ
[    3.318734] Padding  000000000190e5e2: 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a  ZZZZZZZZZZZZZZZZ
[    3.328212] Padding  000000005a23dcab: 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a 5a  ZZZZZZZZZZZZZZZZ
[    3.337942] FIX kmalloc-128: Object at 0x00000000625bf16f not freed
[    3.344217] ds90ux9xx: (i2c_chnl=0x7,i2c_addr=0x2c) failed initialize chip interface, software reset is needed
```

Another useful tool is the `initcall_debug` boot loader setting, but this needs to have a debug kernel configuration.

## Resolving the core dump address

Compile the Linux kernel in debug mode and make sure that the `vmlinux` with debug symbols 
is located on the device where the core dump is debugged. Utilize the [<linux-src>/scripts/faddr2line.](https://github.com/torvalds/linux/blob/master/scripts/faddr2line)
Pass the address, path to `vmlinux` with debug symbols and the `faddr2line` will return 
the line of source code.
