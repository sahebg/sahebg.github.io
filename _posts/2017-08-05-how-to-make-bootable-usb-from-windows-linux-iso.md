---
layout: post
title: "How to make Bootable USB, for any Operating system or bootable ISO image"
modified:   2017-08-08
categories: [ComputerSceince]
tags: [Operating Systems, Bootable ISO, Windows, Linux]
sitemap:
    priority: 0.7
    changefreq: 'monthly'
    lastmod: 2017-08-01T12:49:30-05:00
image:
    feature: /Utility/usbboot1.png
---
Nowadays burning a DVD with ISO image is tidious process, compare to making a Bootable USB. However in market there are plenty of Bootable usb makes such as Pendrive Linux, Unetbootin, Win32DiskImager etc.
I have compared all of them and have made more than 300 bootable usb drive.

- Some of them fails to boot or some of them throw error during Operating System installation.

![_config.yml]({{ site.baseurl }}/images/Utility/1.JPG)

In my experience, Rufus and Win32DiskImager are best Bootable USB maker for any kind of iso(Windows, Ubuntu, Debian, Other linux flavors, Norton Recovery etc).
Here is a simple guide to make a bootable USB drive using Rufus :

- Download latest version of Rufus from this link 
[a link](https://rufus.akeo.ie/)
- Double click the exe and run
- When Rufus opens follow only this Two steps:
    - Select the USB Drive in the Device dropdowm
    - Click on the Select image button beside the ISO Image in Dropdown.
    - After you have selected the ISO image some of the settings (like File system, Cluster size) will automatically take optimized value(NO NEED TO CHANGE ANYTHING)
    ![_config.yml]({{ site.baseurl }}/images/Utility/2.JPG)
    - Then hit Start
 - After that is completed, you can reboot and go to BIOS to boot from USB device.

For making bootable iso from Ubuntu or any other linux you may use UnetBootin.
- Goto this page for downloading required flavor of UnetBootin [a link](https://unetbootin.github.io/linux_download.html)
- Then just follow the image below as selected
  ![_config.yml]({{ site.baseurl }}/images/Utility/3.JPG)
Please comment below in case of any problem found during running the code or any other doubts.
