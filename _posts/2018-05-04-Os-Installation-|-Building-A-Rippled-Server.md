---
published: true
weight: 4
---
First I installed the cachecade hardware key on the 9260-4i.  Then replaced the Perc h700 controller that came with server (bonus) using the 9260-4i with the existing SAS cable to the SAS-A port on the backplane.  During the first boot I installed all the firmware/BIOS updates from Dells website to the latest versions.  

Using the WebBIOS on the RAID controller I created two RAID5 drive groups, one 100GB for the OS and the other with the remaining storage for the database. A 64KB stripe size is recommended.  Also while in WebBIOS I created the CacheCade volume in a RAID1 mirror with write back enabled.  When creating your RAID volumes keep in mind there are optimum settings which can be changed later, either remotely with the MegaRAID Storage Manger or locally with MegaCLI, but the stripe size cannot be changed and should be set to 64KB.  (See this page for MSM and MegaCLI installation on CentOS 7.)  You can choose between the Optimum settings for CacheCade or Fastpath for your use case using this document.  I chose the CacheCade optimum settings for both RAID5 VD's using these settings:  Write Policy=Write Back, Read Policy=No Read Ahead, IO Policy=Cached IO, Access Policy=Read Write, Disk Cache Policy=Disabled, and Background Initialization=Enabled.

CentOS 7 is my OS of choice or RHEL at the enterprise level.  At this point using a usb drive I booted and installed CentOS 7 to the 100GB Partition letting the Installer use the defaults of XFS and an LVM.  We will configure the 8TB volume later using cockpit.  Create a user account during the install process so you can sudo up instead of using the root user, per best practice.  Also enable networking during installation and remember the IP address.  After booting to CentOS for the first time, connect via SSH to your server using putty or terminal.  To find your IP address you can use the "ip addr" command on the terminal if you cannot remember it.  

**Update the OS and reboot.**

	$ sudo yum update -y && sudo init 6

**After the reboot I installed the epel repo and cockpit:**

	$ sudo yum install epel-release && sudo yum update -y
	$ sudo yum install cockpit cockpit-networkmanager cockpit-storaged

**Start and enable Cockpit**

	$ sudo systemctl start cockpit
	$ sudo systemctl enable cockpit

**Configure the firewall**

	$ sudo firewall-cmd --add-service=cockpit
	$ sudo firewall-cmd --add-service=cockpit --permanent
	$ sudo firewall-cmd --reload

Connect your web browser to Cockpit at https://<your server ip>:9090 and login with your user account.

Time to configure the 8TB VD for an LVM formatted with XFS.  After researching which file system would be best for 4K database reads and writes I settled on XFS over BTRFS.  The main logic behind XFS was performance, OS Support, and the fact BTRFS will be removed RHEL 8.

	Placemark for new content

Now we are ready to install rippled.


**Previous Section: [Benchmarking](https://subreddit.github.io/Benchmarking-Building-A-Rippled-Server/)**

**Next Section: Installing rippled**
