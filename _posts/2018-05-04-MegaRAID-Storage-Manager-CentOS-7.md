---
published: true
---
**Install MSM - Server component only for remote managment**

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
