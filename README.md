smartos-platform-upgrade
========================

A script to simplify upgrades of USB booted SmartOS installations.

Installation
------------

Drop the script in `/opt/local/bin` on the GZ.

Usage
-----

Run the script. It'll find the USB stick, download the latest platform from
Joyent, do the upgrade and report its status. The download and update platform
stages will probably take a few minutes each.

```
[root@00-25-90-7d-03-8b ~]# platform-upgrade
Checking current boot device... detected /dev/dsk/c0t0d0p1, mounted, OK
Downloading latest platform... OK
Verifying checksum... OK
Extracting platform... OK
Updating platform on boot device... OK
Activating new platform on boot device... OK

Boot device upgraded. To do:

 1) Sanity check the contents of /tmp/tmp.KCaawL/usb
 2) umount /dev/dsk/c0t0d0p1
 3) reboot
[root@00-25-90-7d-03-8b ~]# 
```

Once the upgrade is done, verify that the contents of the USB stick looks sane,
unmount it and reboot to the new platform.

```
[root@00-25-90-7d-03-8b ~]# ls -l /tmp/tmp.KCaawL/usb
total 24
drwxrwxrwx   1 root     root        4096 Jan  3  2011 boot
drwxrwxrwx   1 root     root        4096 Dec 28 16:03 platform
drwxrwxrwx   1 root     root        4096 Dec 28 15:24 platform.old
[root@00-25-90-7d-03-8b ~]# ls -l /tmp/tmp.KCaawL/usb/platform
total 9
drwxrwxrwx   1 root     root        4096 Dec 28 16:03 i86pc
-rwxrwxrwx   1 root     root          17 Dec 28 02:40 root.password
[root@00-25-90-7d-03-8b ~]# umount /dev/dsk/c0t0d0p1
[root@00-25-90-7d-03-8b ~]# reboot
```

By default, the first removable device found is assumed to be the boot USB
stick. If this is not the case, the correct device name can be given on the
command line:

```
[root@00-25-90-38-94-04 ~]# platform-upgrade /dev/dsk/c1t0d0p1
Checking current boot device... using /dev/dsk/c1t0d0p1, mounted, OK
Downloading latest platform...
```

