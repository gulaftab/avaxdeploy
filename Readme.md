## AvatarPro Deployer



### Quick Start

Assuming Ansible is already installed and configured
* Run the deployment playbook

```ansible-playbook -v -i hosts deploy.yml```


## Installation Guide

### Requirements


In order to deploy your application , you will need:

* Ansible in your deployer machine
* Ansible uses the pywinrm package to communicate with Windows servers over WinRM. If not already installed you install it by running the following 
``` pip install "pywinrm>=0.3.0" ```

### On Windows Side (First Time only) 

Unlike Linux/Unix hosts, which use SSH by default, Windows hosts are configured with WinRM

* WinRM is enabled by default, but in most cases extra configuration is required to use WinRM with Ansible. 

* On your windows machine, Run the following commands in your powershell to configure windows hosts to be supported by Ansible.  For more Info [Ansible Docs](https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html#winrm-setup)


``` 
$url = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
$file = "$env:temp\ConfigureRemotingForAnsible.ps1"

(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)

powershell.exe -ExecutionPolicy ByPass -File $file
```

### Install dependencies

First install the required

```
 $ ansible-galaxy collection install -r requirements.yml
 
 ```

### Deploying


In order to deploy with Ansistrano, you need to perform some steps:

* Create a new `hosts` file. Check [ansible inventory documentation](http://docs.ansible.com/intro_inventory.html) if you need help. This file will identify all the hosts where to deploy to. 
* Set up role variables in file `group_vars/all.yml`

* Run the deployment playbook

```ansible-playbook -v -i hosts deploy.yml```
