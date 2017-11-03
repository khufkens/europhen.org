---
layout: page
title: "Quick Install Guide"
meta_title: ""
permalink: "/installation/quick-install/"
header: no
---

## Download the required software

- [download Stardot Tools](http://www.stardot.com/downloads)
- [download the PhenoCam Installation Tool (PIT)](https://github.com/khufkens/phenocam-installation-tool/archive/master.zip)
 and unzip the archive

## Configure the camera

Get all necessary hardware for a lab setup. It is always advisable to run the installation of the camera in the lab, rather than in the field (where trouble shooting network issue, the number one cause of failure, is hard).

### gather hardware components

- Power over Ethernet (PoE) injector
- an ethernet surge protector
- an ethernet hub connected to the computer used to download the software (or a shared network between the camera and the computer containing the software previously downloaded).
- 4 (short) ethernet cables

#### Hardware connections

1. connect the ethernet hub with the in port of the PoE injector
2. connect the PoE out port with the cable leading to the surge protector
3. connect the surge protector to the camera (note the surge protector sits just before the camera using only a short cable)
4. make sure your computer is connected to the ethernet hub or shares the network with the camera

#### Identifying the camera on the network

1. start Stardot Tools
2. hit the refresh button
3. find your camera in the list
4. write down the IP address

You will need the IP address in the next step in order to identify the camera to install software to.

#### Pushing the correct settings to the camera

Now open a terminal (in windows you find the program called cmd, in OSX and Linux open a terminal). Move into the directory which contains the PIT.sh and PIT.bat files. Now to push the settings to the camera use the following syntax for the command line PIT.sh and PIT.bat scripts.

```
sh ./PIT.sh IP USER PASSWORD CAMERA TIME_OFFSET TZ CRON_START CRON_END CRON_INT FTP_MODE
```

Or from a Windows command prompt:

```
PIT.bat IP USER PASSWORD CAMERA TIME_OFFSET TZ CRON_START CRON_END CRON_INT FTP_MODE
```

For central European time (CET) this would be:

```
./PIT.sh  xyz.xyz.xyz.xyz admin admin testcamera3 +1 4 22 30 active
```

The program will run, and give verbose feedback on the progress. If the process hangs, reset the camera and try again.

## Customize camera settings

Custom settings are sometimes necessary, mainly if you want to specify a server which is different from the current default (phenocam.sr.unh.edu, the PhenoCam US network). Other changes can include the timing when pictures are taken. Normally this is done at random at user specified intervals. When running on batteries having this fixed is preferred.

### Accessing camera settings manually

 1. Open StarDot tools
 2. Find your camera
 3. double click on the camera, which will take you to the homepage of the camera then log in using your camera password admin / admin

### Changing the camera password

Go to the security tab to change the default password (admin/admin) into a secure password not prone to brute force attacks (minimum 8 characters in length (A-z,0-9), including a special character).

![](../../images/documentation/password.png)

### Manual config of a custom server

Go to the Advanced tab and select the Manual Config tab within.

![](../../images/documentation/server_settings.png)

Edit the server settings by either entering an IP address or a server url.

![](../../images/documentation/server_settings_edit.png)

After altering configuration files always push the "Save" button to make changes permanent between reboots of the camera.