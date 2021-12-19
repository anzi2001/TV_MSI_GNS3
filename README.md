
Provisioning script to launch a GNS3 virtual machine,
ready to be available at Vms IP address

Credentials for guacamole:

> username: TV
> password: tehnicne2021

Credentials for user student:


> username: student
> password: tehnicne2021


Credentials for direct xrdp access is forbidden with ufw
Only ports 80, 443 and 22 are allowed to the external world


## Cloud init:
	Running with multipass: 
		- cd to cloud-init directory
		- `multipass launch -c 4 -d 10G -m 4G --name gns3 --cloud-init cloud-init.yaml`
	
	Giving the virtual machine more ram and cpu is optional but greatly increases provisioning speed

	Virtual machine should now be acessible trough https://vmip

	


## Vagrant:
	Running with vagrant:
		- cd to vagrant directory
		- `vagrant up`
		- virtual machine is accessible through https://localhost:4433

	Currently, the vagrant setup produces a black screen when logging in with guacamole

### Setup process:
	- add "-no-install-recommends" for quicker installs with less packages
	- add groups needed, ubridge is not added since it has to be a system group
	- add xrdp user and add it to ssl-cert group
	- add student user, give sudo permissions and add necessary groups, additionally add ssh keys of me and matjazp
	- install all packages
	- write needed configuration files 
	- add student to ubridge
	- create self-signed ssl certificates, restart nginx
	- create a docker volume, add user-mapping.xml
	- run guacd, guacamole
	- forbid all ports except 80,443,22 from outside world
	- allow 3389,4882,8080 ports only on localhost 
	- add gns3 to autostart