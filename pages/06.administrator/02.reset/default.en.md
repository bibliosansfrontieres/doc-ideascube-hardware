---
title: 'Soft & Hard reset'
---

It can be handy to reset the device at some point (operating system that does not work as expected)

Two method are available to reset the device : soft reset and hard reset

## Soft reset

The [following bash script](https://gitlab.com/bibliosansfrontieres/olip-bsf/cap/factory-config/-/blob/master/reset.sh) reset "softly" the device. This script can not fix any damaged operating system.

It will perform the following action : 

* re-establish the factory configuration
* set back password for `cap` user
* stop & disable & remove VPN (optional)
* remove SSH key pairs and `authorized_keys` files (optional)
* stop & disable & remove Balena Engine (and their related Docker images / container / networks / etc)
* umount & format the external hard drive

It must be executed, **as root**, this way :
```
curl -sfL https://gitlab.com/bibliosansfrontieres/olip-bsf/cap/factory-config/-/raw/master/reset.sh | bash
```

## Hard reset

The following procedure perform a "hard" reset and will put the device back in a factory state **without** formating the external hard drive. **You'll have to do it manually if needed!**

### Prepare the USB key

1. Download the [recovery image](http://drop.bsf-intranet.org/clonezilla-live-RC-RC02.8_silent.zip) (~900MB)
2. Unzip the file. You get a `clonezilla-live-RC-RC02.8/` directory, which in turn contains a few files and directories:

```
clonezilla-live-RC-RC02.8
├── boot
├── Clonezilla-Live-Version
├── EFI
├── GPL
├── home
├── live
├── syslinux
└── utils
```
3. Place **all of these subdirectories** at the root of an USB drive.

When looking at the root of your USB key, you should only see these files and folders:

`boot/ Clonezilla-Live-Version EFI/ GPL home/ live/ syslinux/ utils/`

### Proceed to reset

The device must be turned off.

4. Plug the RECOVERY USB drive on the USB port of the device and power it
5. The recovery will be processed automatically and the device will auto-shutdown when finished (LED indicator off)
6. Start the device again and wait until the latter shutdown one more time
7. Done! You can remove the USB key and use the device

### Format the HDD manually

If you want to push the reset further and delete all installed contents/applications, you can format the external HDD:

```
umount -A -l /dev/sda1
mkfs.ext4 -F /dev/sda1
```
