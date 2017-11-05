---
layout: page-fullwidth
title: "Detailed Installation Guide"
subheadline: ""
teaser: "a detail description on how to install a PhenoCam"
permalink: "/installation/protocol/"
header: no
---
<div class="row">
<div class="medium-4 medium-push-8 columns" markdown="1">
<div class="panel radius" markdown="1">
**Table of Contents**
{: #toc }
*  TOC
{:toc}
</div>
</div><!-- /.medium-4.columns -->

<div class="medium-8 medium-pull-4 columns" markdown="1">

# General Information
You can find an overview of the {{site.title}} network at:

[{{site.url}}/about/]({{site.url}}/about/)

This configuration guide is specific to StarDot cameras, the preferred camera to use for phenological monitoring.  They contain an embedded version of Linux and are capable of complex automated custom configurations. Our default configuration will set up the camera to upload images to the {{site.title}} server on a regular schedule throughout the day.  We have deployed these StarDot cameras in a wide variety of environments and have found them to be very robust and reliable.  For more information on specific configurations you can check:

[{{site.url}}/installation/tools/]({{site.url}}/installation/tools/)

We highly recommend configuring the camera in a lab with stable power and network connections before deployment.  Once the camera is configured, testing with the network equipment which will be installed in the field (while still in the lab) is also recommended.

The manuals for StarDot cameras are available here:

[http://www.stardot.com/manuals](http://www.stardot.com/manuals)

The manual is quite detailed and has lots of additional information on camera configuration.

# Camera configuration, network & power connections

## Supplying Power and Network to the Camera

In the figure to the right a typical lab setup for configuring a camera is shown.  We typically use a small network hub connected to the local network so that we can have the camera and another computer connected to the same network.  The camera has a power light indicator on the front and it should be lit.  The Ethernet connector on the back of the camera also has a light which indicates whether the Ethernet port link has been established.  The camera by default is configured to get its network address from a DHCP server so the network hub should be connected to a network with a DHCP server 

### Power-over-Ethernet (PoE)

If your site has AC line power, then we will have provided you with a PoE (power-over-ethernet) injector (illustrated in the photo on the right), which plugs into the wall and which allows power to the camera to be sent over the standard ethernet (cat 5, 5e, 6) cable which we have sent you. One end of the ethernet cable goes to the surge protector, the other to the “data & power out” socket on the POE injector. Then connect one end of a short Ethernet cable to the “data in” socket on the POE injector, and the other to your network hub. Then plug the POE injector into an electrical outlet.

### Combination Ethernet/Power Cable

If your site uses DC power (solar, generator, etc.), then we will have provided you with a special combination Ethernet/power cable (the white cable in the picture above). This eliminates the need for a separate power cable to the camera. The end with the male power jack goes to the camera (plug the power jack into the socket on the back of the camera, and plug the ethernet connector into to the surge protector, and then a short cable from the surge protector to the camera). The end with the female power jack has a male jack with two terminals (marked + and -) attached. Run a wire from this jack to your battery bank (the red and black wires in the picture on the right). Before connecting power, however, plug the Ethernet connector into your network hub, as the camera requires an Ethernet connection when it is powered up. Note that when you use the combination Ethernet/power cable, or a separate 12 V DC power cable, it is still possible for lightning damage to occur to the camera even when you use an Ethernet surge protector. This is why we recommend powering the camera via POE if possible.  When testing in the lab, you can use a 12V power supply, a battery, or for configuration purposes a POE injector as described above.  Or simply use the separate power adapter that came with your camera.

## Finding the camera on your network

Once your camera is powered on and connected to the network you will need to find your camera’s network IP address.  To do this you will use another computer connected to the same LAN as the camera.  First verify that the computer you are using was able to connect to the network and get an IP via DHCP.  If this is not the case, you may need to get help from the local network admin with your setup. 

The easiest way to find the camera’s IP address is to install StarDot Tools from the CD included with the camera (Windows only, sorry).  Run the program and click "refresh".  The camera should be detected and the camera’s IP address shown (you may have to run Tools as administrator in Windows, depending on your settings). See the Troubleshooting section below if the IP address is not automatically detected.  

If you are configuring your camera with a non-Windows computer there are other things you can do to find the IP address of the camera.  From a Linux or Mac OS X terminal window you should be able to type the following command:

	arp -a

to get a list of the MAC addresses and IP’s of all the computers on the local network.  The StarDot cameras have a MAC address that starts with 00:30 so you may be able to find the camera that way.  Again, you may need help from the local network administrator for this step.

In either case, you should then be able to enter the camera’s IP address into your internet browser’s address bar and a page should load with a blue background and a live image from the camera.

Most routers are configured to hand out addresses via DHCP so the camera will usually join the LAN once plugged in.  In some cases, the local router may limit network access based on a list of MAC addresses. If this is the case you may need to add the camera’s MAC address to a list of “approved devices” for your network.  The MAC address is the same as the serial number printed on the bottom of the camera. 

## Change the camera’s default password

Once you can connect to the camera with a computer the first thing you should do is change the default password.  When using a university public IP address, we have had a camera hacked within 2-3 minutes of being connected to the network.  If you are on a local private network behind a router or firewall you are probably safe but we recommend changing the password as soon as possible.  Here are the steps:


- Point your browser at the camera’s IP address
- Click the "config" link at the bottom of the live camera image
- Log in as user "admin", password "admin”
- Go to the “Security” tab of the interface 
- Modify the “admin” password using the form.

{% include alert info="Note: If your camera is connected directly to the Internet, and can be accessed from anywhere in the world, then it is essential that the password be changed to something that is secure.  If you change the password, please note that the PhenoCam Install Tool only works with alphanumeric passwords."%}

{% include alert alert="Because of DynDNS cyberattacks that leverage security vulnerabilities (e.g. https://securityledger.com/2016/10/dhs-warns-of-mirai-malware-threat-to-cell-gateways/) in numerous internet-attached devices, we strongly encourage you to ensure that all devices (no matter how small — i.e. including but not limited to cell modems, routers, data loggers, cameras, printers, etc.) with an internet connection have been re-programmed with secure passwords and active firewall settings wherever possible, so as to minimize the likelihood of your devices becoming part of a botnet. Please re-program your camera password when the camera is not on an open network connection (i.e. when it is only on a local network connection) as infection rates are fast (~2-3 min.). If needed, you can use the 'reset' button on the back of the camera to restore all factory settings, and then re-program the password. Once the password is secure, then you can safely proceed to configuring the camera using the PIT. If you have any questions, please do not hesitate to contact us."%}

## Filling out the site survey
Before running the PhenoCam Installation Tool (PIT) you will need to have a site established with us.  Filling out the site survey provides us with some basic site-level metadata.  If you don't have answers to some of the questions you can leave them blank and send us an e-mail at a later time with this information.  The critical information (sitename, site contacts, location, etc.) is helpful for us to set up the site.  Once you have filled out the survey drop us an e-mail and we will prepare the server directories for your site.   


## Running the PhenoCam Installation Tool (PIT)
While the camera's web interface is useful for manual configuration we have developed a set of scripts which by-pass the web interface and alter many of the camera's default settings.  This includes installing custom scripts to upload images and associated metadata to our server. 

To run the PIT you will need the IP address of the camera, the admin password, and a name for you site/camera.  Before proceeding you should work with us to establish a site name and fill out the site survey. 

### Downloading the PIT
You will need to download the PhenoCam Install Tool (PIT), which you can find here:

[https://khufkens.github.io/phenocam-installation-tool/](https://khufkens.github.io/phenocam-installation-tool/
)

You will need to download (either a zipfile or tar archive of) the package and extract it to a directory/folder on your computer.  The PIT contains main two scripts: PIT.bat and PIT.sh.  If you are configuring your camera from a windows machine, you will just run PIT.bat.  On Linux or OS X you will need to run PIT.sh.  In either case you will run the script from a command shell or terminal window.


### Checking network access to our server
The PIT scripts need to connect to the PhenoCam server (xyz.xyz.xyz.xyz).  You should verify that you can connect to the server from the computer you will be doing the configuration from. If your computer can't contact our server chances are good that the camera won't be able to either. Connecting to our website with a browser should be possible.

To verify that your computer can also FTP a file to the server you can use any FTP client available on your computer. You can connect to the server using anonymous FTP, change directories to your camera's data directory (data/<sitename>/) and transfer a file. Below is a sample session using a command line FTP client from a OS X terminal window:

{% include alert info="Directory listing (the 'ls' or 'dir' FTP commands) on the server are not permitted. So some FTP clients (especially ones with a graphical user interface) like FileZilla will generate lots of errors.  You may have to look carefully to see a 'Transfer complete.' message from the server."%}

If you can connect to our server with a web browser but cannot transfer files via FTP, you are likely encountering a network firewall issue. The FTP protocol is not secure (passwords are sent in clear text over the network) so it is often blocked by a site's firewall. Within the FTP protocol there are two connection modes, ‘ACTIVE' and 'PASSIVE', available for a transfer.  Often only one (usually 'PASSIVE') or the other will be allowed to pass the firewall.  To change the connection type use the FTP command 'pass'. This command toggles between connection types so is used for both modes. The default mode may depend on the FTP client you are using.


### Running the PIT
Once you've verified that your network connection is good and that you can communicate with both the camera and our server you are ready to run the PIT script.  A detailed description of running the script is found on the GitHub page.  For convenience we summarize the procedure here.

The PIT script is run from the computer being used to configure the camera.  To run the script you will need a window in which to type commands (cmd.exe on windows or a terminal window on Linux or OS X). The basic command from a Linux or OS X terminal is:

```bash
sh ./PIT.sh IP USER PASSWORD CAMERA TIME_OFFSET TZ CRON_START CRON_END CRON_INT FTP_MODE
```

Or from a Windows cmd.exe prompt:

```
PIT.bat IP USER PASSWORD CAMERA TIME_OFFSET TZ CRON_START CRON_END CRON_INT FTP_MODE
```
{% include alert info="If you are running a post-XP Windows operating system, the telnet program, on which the PIT depends, is not available by default.  Alternatively,  you can consult [Microsoft's help pages](https://social.technet.microsoft.com/wiki/contents/articles/38433.windows-10-enabling-telnet-client.aspx) to enable the telnet command."%}

The parameters required to run the script are described below:

| Parameter | Description |
------------|-------------|
IP | IP address of the camera |
USER | user name (admin - if not set)
PASSWORD | user password (on a new StarDot NetCam this is admin, but hopefully you’ve already changed it!)
CAMERA | the name of the camera / site
TIME_OFFSET |  difference in hours from UTC of the time zone in which the camera resides (always use + or - signs to denote differences from UTC)
TZ | a text string corresponding to the local time zone (e.g. EST)
CRON_START | hour to start the scheduled image acquisitions (e.g. 4 to start collecting images at 4 in the morning)
CRON_END | hour to end the scheduled image acquisitions (e.g. 22 to end collecting images at 10 in the evening)
CRON_INT | interval in minutes at which to take pictures (e.g. 15, for every 15 minutes - default PhenoCam setting is 30)
FTP_MODE | active or passive (default = passive)

An example of the command for a test camera configuration is given below:

```bash
./PIT.sh 140.247.89.xx admin admin testcam3 -5 EST 4 22 30 passive
```

This configures the camera 'testcam3', located in the EST time zone (UTC -5) to take images every half hour between 4 and 22h.

Here’s a brief summary of what the PIT script will do:

- Sets a default DNS server for the camera
- Sets a default NTP (time) server for the camera
- Sets the image overlay strings
- Sets the default color balance 
- Installs custom scripts to upload images
- If the camera is a standard IR-enabled NetCam, the script will upload
back-to-back IR and RGB images
- The scripts will create and upload a metadata file with each image
Installs a schedule to run these scripts
- Does a one-time run of the script to upload initial images and metadata 

The PIT script is designed to handle all the configuration of the camera.  If it runs successfully, an initial upload of image files is sent to our server.

If the script runs successfully, please do not change any config settings! Changing the FTP settings in particular (or even clicking the box that says “FTP Upload”) will likely cause upload problems. The two exceptions to this recommendation are the camera focus which will still need to be adjusted manually and to configure additional upload servers.  See the deployment section on focusing your camera for more details and the custom server settings below. 

{% include alert info="Note that the scripts that are installed using the PhenoCam Install Tool will not populate the fields on the FTP tab: this is ok!"%}

It is not unusual for the script to encounter some error when run. If this is the case, try to capture the error messages and send them to us. We will be happy to work with you to get your camera properly configured.

When running the PIT you may realize that you’ve used a wrong parameter and need to run the script again.  In principal this should work fine, but the you may encounter errors when rerunning the script.  If this is the case, you can to a hard reset of the camera to factory settings and start over. On the back of the camera there should be a small opening labeled “reset”. Use a paper clip or pin to press the button inside to reset to factory settings.

{% include alert info="This resets the admin password to the default value so don’t forget to change the admin password."%}

## Custom Server Settings

To alter the default server settings and use the {{site.title}} or local servers go to the "Advanced tab" and select the "Manual Config" tab within. Find the server.txt file and click edit.

![](../../images/documentation/server_settings.png)

Edit the server settings by either entering an IP address or a server url. Data for {{site.title}} should use url: **{{site.dataurl}}**. Multiple servers are allowed by entering their respective IP or url on separate lines.

![](../../images/documentation/server_settings_edit.png)

After altering configuration files always push the "Save" button in the main "Manual Config" tab to make changes permanent between reboots of the camera.

# Camera Deployment

## Camera Housing Installation

The camera housing we typically use is a Vitek (model VT-EH10) Indoor-Outdoor Enclosure.  It will cost about $35 (the price seems to fluctuate, between $25 and $50.)  Anything similar to this should be fine.   There is a sliding mount inside the housing to which the camera attaches with a short screw. This is usually a ¼-20 screw (which is included with the housing), but some cameras have shipped recently with M6 threads (if we sent you a camera with M6 threads, we should have also included an M6 screw). The sliding mount snaps in to the rails on the bottom of the housing. Please remember to remove the camera's lens cap before installing the camera! Note that the camera should be slid forward in its housing, so the lens is almost touching the window, to minimize the potential for reflections.
 
## Camera Field Installation

Here are some basic guidelines to keep in mind during camera deployments:

- Phenology is one goal, but we'd also like good-looking pictures.
- The camera should be pointed north to minimize lens flare and shadowing. 
- The image should include a horizon, but the image should be more than 50% canopy and less than 50% sky; the ideal mix is about 20% sky, 80% canopy).
- The camera should point somewhat below the horizontal to obtain maximum canopy coverage and also spatial integration (a mounting height of 5-10 m above the canopy is generally good, but the specifics may depend on the nature of your tower, length of cables, etc.).
- Secure mounting and a stable field of view over time are essential for getting high quality data.  Be sure to mount the camera in such a way as to minimize any camera movement, in a location that is unlikely to be disturbed. Make sure that all screws and nuts are tightened, and that the housing is securely latched closed. Plug large holes in the housing with putty to prevent spiders and yellow jackets from moving in.

## Focusing the Camera

Focusing works best on a sunny day with a nearby laptop connected to the camera's configuration pages. Cameras are focused in the lab before being shipped, but during deployment you will probably want to fine-tune the focus depending on the distance from the camera to the vegetation of interest.  We recommend practicing this procedure in the lab so that you are familiar with the procedure prior to deployment.

If you want to adjust the focus, this is best accomplished while viewing the camera image on a laptop.  You will want to do this with the camera mounted on the tower so that you can verify that the field of view is as desired. The standard lens we recommend is the 6.2 mm, which is relatively easy to focus, as it has just a single focus knob. The 4-10 mm zoom lenses sold by StarDot can yield great images, but with zoom, iris, and focus, they can be much more difficult to focus. 

Here are the basic steps for adjusting the camera focus:

- On the camera's config pages, change "Resolution" to "688x480 NTSC Focus Mode" (last option in the drop-down under Image -> Processing) and hit "APPLY".
- Click on "Pop-up Live Image" in the upper right-hand corner to open a large image. In focus mode, only a fraction of the total image is displayed, but this way the refresh rate is very fast and it is quite easy to get the focus very sharp.
- Adjust the focus ring (it can be quite sensitive) so that the image is sharp. You may find it helps to focus on a specific object in the image – such as a branch. Tighten the screw on the focus ring when finished. Change the resolution back to its original value ("1296x960 QFULL*", see reference image below) and hit "APPLY".

