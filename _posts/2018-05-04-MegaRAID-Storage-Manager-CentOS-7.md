---
published: true
weight: 10
---
The MegaRAID Storage Manager is a nice GUI tool that will you change your RAID volume settings on the fly.  Fortunatley there is an option to remotely manage the RAID controller from another workstation with a desktop envrionment by installing only the server portion of MSM.  You could also manage the RAID controller locally on the server using MegaCLI.  The choice is yours.

**Installing MegaRAID Storage Server - Remote Server Package only**

Install the prereqs:

	$ sudo yum install csh net-snmp net-snmp-utils

Download MegaRAID Storage Manager from broadcom and accept the EULA.  SCP the file to your server and extract.

	$ tar zxvf 17.05.00.02_Linux-64_MSM.gz
	$ cd disk
	$ sudo ./install.csh -d -ru popup
	$ sudo systemctl daemon-reload
	$ sudo systemctl status lsi_mrdsnmpd

Add the necessary Firewall Rules
	$ sudo firewall-cmd --zone=public --add-port=3071/tcp --permanent
	$ sudo firewall-cmd --zone=public --add-port=3071/udp -permanent
	$ sudo firewall-cmd --zone=public --add-port=5571/udp --permanent
	$ sudo firewall-cmd --reload

Now Install the MegaRAID client on a workstation to manage the RAID controller remotely using the hostname or ip of your server.



**To install MegaCLI download the software from broadcom and accept the EULA.**

	$ unzip 8-07-14_MegaCLI.zip
	$ cd Linux
	$ sudo yum install MegaCli-8.07.14-1.noarch.rpm
	$ cd /opt/MegaRAID/MegaCli
	$ ./MegacCli64## A New Post
