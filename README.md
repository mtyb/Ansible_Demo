# Needed software:
- VirtualBox (tested on version 7.04) - https://www.virtualbox.org/wiki/Downloads
- Vagrant (tested on version 2.3.3) - https://developer.hashicorp.com/vagrant/downloads

# Optional software:
- MobaXterm (for SSH connection to Ansible VM) - https://mobaxterm.mobatek.net/download.html

# Repo overview:
1) vagrantfile
2) playbooks directory

Vagrantfile creates 4 Virtual Machines:
- 2 Almalinux VMs - Ansible VM and Grafana VM and 
- 2 Windows Server 2019 VMs. 
All of the VMs will be connected to a private network. 

Playbooks directory contains:
- inventory directory, which contains 
	- hosts.ini
	- group_vars directory 
- roles
- playbooks

``` hosts.ini ``` - contains IP addresses for all mentioned Virtual Machines. Each IP address is assigned to specific hosts group. 

``` group_vars ``` - contains directories with specific hosts group variables

``` role ``` - set a playbooks for deploying specific sets of tasks

``` playbook ``` - single playbook invoking specific tasks or specific role

# Usage:
- navigate to repo main directory
- open powershell
- type: vagrant up
- wait till Vagrant finishes creating VMs
- log to Ansible VM (default username and password for all Vagrant VMs - Login: vagrant Password: vagrant)

# Examples:
Log to Ansible VM.
Change directory: 
```
cd playbooks
```

To ping all Windows Virtual machines:
```
ansible -m win_ping os_win -i inventory/hosts.ini
```

To ping all Linux Virtual machines:
```
ansible -m ping os_linux -i inventory/hosts.ini
```

To install applications using configure_windows.yaml type:
```
ansible-playbook configure_windows.yaml -i inventory/hosts.ini
```

To install Vim on the Ansible VM using Ansible pull:
```
ansible-pull -U https://github.com/mtyb/Ansible_Demo.git  /playbooks/installSemaphore.yaml
```

To limit deployment scope to specific VM from inventory run:
```
ansible-playbook -i inventory/hosts.ini installApps.yaml --limit=10.11.12.241
``` 