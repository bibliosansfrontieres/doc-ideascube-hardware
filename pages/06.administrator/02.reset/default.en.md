---
title: 'Soft & Hard reset'
---

It can be handy to reset the device at some point (operating system that does not work as expected)

Two method are available to reset the device : soft reset and hard reset

## Soft reset

The [following bash script](https://github.com/bibliosansfrontieres/ideascube-deploy/raw/master/reset.sh) reset "softly" the device. This script can not fix any damaged operating system.

It will perform the following action : 

1. re-establish the factory network configuration
2. set back password for `cap` user
3. stop & disable & remove VPN
4. stop & disable & remove Balena Engine (and their related Docker images / container / networks / etc)
5. umount & format the external hard drive
6. finally reboot the device

It must be executed, **as root**, this way :
```
curl -sfL https://github.com/bibliosansfrontieres/ideascube-deploy/raw/master/reset.sh | bash
```

## Hard reset

The following procedure perform a "hard" reset and will put the device back in a factory state **without** formating the external hard drive. **You'll have to do it manually if needed !**

1. Download the [recovery image](http://drop.bsf-intranet.org/clonezilla-live-RC-RC02.8_silent.zip)
2. Unzip the file and place it at the root of an USB drive
3. Plug the RECOVERY USB drive on the USB port of the device and power it
4. The recovery will be progressed automatically and it will auto-shutdown when finish (LED indicator off)
5. Start the device and wait until the latter shutdown one more time
6. Done ! You can power and use the device

### Format the HDD manually
```
umount -A -l /dev/sda1
mkfs.ext4 -F /dev/sda1
```
