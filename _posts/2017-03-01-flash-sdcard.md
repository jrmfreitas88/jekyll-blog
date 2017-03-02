---
layout: post
title:  "Flashing the SD Card"
date:   2017-03-01 23:22:08 +0000
categories: jekyll update
---

# Description
This guide aims to describe how to flash the Raspbian distribution on a SD Flash Card with SSH enabled.

# Steps
1. Create Temporary Folder
```
mkdir ~/Desktop/raspbian
```

1. Change Directory
```
cd !$
```
__Note:__ `!$` is a shortcut for the last parameter used on the last command, which would be "~/Desktop/raspbian" in this case.

1. Download Raspbian Image
```
wget https://downloads.raspberrypi.org/raspbian_lite_latest
```
__Note:__ If you don't need graphical environment, I would suggest downloading the lite version.

1. Identify SD Card
```
diskutil list
```

1. Unmount SD Card
```
diskutil unmountDisk /dev/disk2
```

1. Flash SD Card
```
sudo dd bs=1m if=~/Desktop/2016-11-25-raspbian-jessie-lite.img of=/dev/disk2
```

1. Check Progress Status (Optional)
```
[ctrl] + t
````

1. Enable SSH
```
touch /Volumes/boot/ssh
```

1. Eject
```
diskutil eject /dev/disk2
```

# References
* [https://www.raspberrypi.org/documentation/installation/installing-images/mac.md][raspberry-flash-guide]

[raspberry-flash-guide]: https://www.raspberrypi.org/documentation/installation/installing-images/mac.md