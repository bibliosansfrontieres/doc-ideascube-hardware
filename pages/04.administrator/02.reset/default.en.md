---
title: 'Hardware reset'
---

I can be useful to reset the device if the operating system does not work as expected.

Theire is two ways to reset the device : soft reset and hard reset

## Soft reset
The [following bash script](https://github.com/bibliosansfrontieres/ideascube-deploy/raw/master/reset.sh) reset "softly" the device. This script can not fix any damaged operating system.

1. re-establish the factory network configuration
2. set back password for `cap` user
3. stop & disable & remove VPN
4. stop & disable & remove Balena Engine
5. umount & format the external hard drive
6. finaly reboot the device

It must be executed this way :
```
curl -sfL https://github.com/bibliosansfrontieres/ideascube-deploy/raw/master/reset.sh | bash
```

## Hard reset

The following procedure does an "hard" reset of the device **without** formating the external hard drive. **You'll have to do it manually if needed !**

1. Download the [recovery image](https://mega.nz/#!14AxDIQA!uweEwRo8RwQGBcvxsFHWKURVchSHthn2uysF5X60Bok)
2. Unzip the file and place it at the root of an USB drive
3. Plug the RECOVERY USB drive on the USB port of the device and power it
4. The recovery will be progressed automatically and it will auto-shutdown when finish (LED indicator off)
5. Start the device and wait until the latter shutdown one more time
6. Done ! You can power and use the device
