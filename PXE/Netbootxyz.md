---
title: Netbootxyz
description: 
published: 1
date: 2024-06-15T02:26:59.763Z
tags: netbootxyz,pxe,boot,betwork
editor: markdown
dateCreated: 2024-06-15T02:26:59.763Z
---

# Cloud-Init Booting

### Creating an Ubuntu 22.04 Cloud-Init Auto Installation

`user-data`

```
#cloud-config
autoinstall:
  version: 1
  identity:
    hostname: ubuntu-server
    password: "$6$exDY1mhS4KUYCE/2$zmn9ToZwTKLhCw.b4/b.ZRTIZM30JZ4QrOQ2aOXJ8yk96xpcCof0kxKwuX1kqLG/ygbJ1f8wxED22bTL4F46P0" # ubuntu
    username: ubuntu
```

`menu.ipxe`

```
#!ipxe

:global_vars
# set location of custom netboot.xyz live http assets
set live_endpoint http://pxe.inside.lan:8080

:main_menu
clear menu
menu ipxe All The Things
item --gap Default:
item local ${space} Boot from local
item --gap Distributions:
item ubuntu_ks ${space} Ubuntu Kick Start
choose --default ${menu} menu
echo ${cls}
goto ${menu} ||

:ubuntu_ks
imgfree
kernel ${live_endpoint}/ubuntu22-04/vmlinuz root=/dev/ram0 ramdisk_size=1500000 fsck.mode=skip ip=dhcp url=${live_endpoint}/ubuntu22-04/ubuntu-22.04.4-live-server-amd64.iso autoinstall ds=nocloud-net;s=http://pxe.inside.lan:8000 cloud-config-url=/dev/null
initrd ${live_endpoint}/ubuntu22-04/initrd
boot

:local
echo Booting from local disks ...
exit 1
```