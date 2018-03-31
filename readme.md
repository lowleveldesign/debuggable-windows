
This repository contains Ansible scripts which will install and configure tools necessary to effectively debug and profile applications on Windows.

# Provision Great Debugging Experience on Windows

Table of contents:

- [Requirements](#requirements)
- [How to run the playbook](#how-to-run-the-playbook)
- [What's in the playbook](#whats-in-the-playbook)
- [Contributions](#contributions)

## Requirements

Currently, the scripts support **64-bit** systems only. You will need an Ansible host, which could be [a Linux box](http://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) or [Windows Subsystem for Linux](http://docs.ansible.com/ansible/latest/user_guide/windows_faq.html?highlight=windows%20subsystem#can-ansible-run-on-windows). You also need to configure the Windows machine to meet Ansible requirements as explained in [the Ansible documentation](http://docs.ansible.com/ansible/latest/user_guide/windows_setup.html).

## How to run the playbook

Clone this repository to a folder on your Ansible host. Then edit the **hosts inventory** to add the machines you would like to provision. For each group of hosts you may want to create a separate variables file under the **group_vars** folder where you will store custom settings and user credentials (**ansible_user** and **ansible_password**). *Remember to [encrypt the password](http://docs.ansible.com/ansible/latest/user_guide/playbooks_vault.html) if you plan to store it in the file*. 

The playbook uses the following variables (you may modify them through command line, by adding group variables file, or editing the group_vars/all.yml file):

Variable | Default Value | Description
---------|---------------|-------------
tools_path | C:\tools | A folder where diagnostics tools will be downloaded and saved
symbols_path | C:\symbols | A place for storing cached PDB debugging symbol files
dump_path | C:\dumps | A place where procudmp will store dumps of the crashing applications
choco_apps | [ 7zip, git ] | Chocolatey apps that should be installed while provisioning
git_psmodules_tocheckout | [] | Git repositories that contain PowerShell modules that you want to use. Ansible will checkout them in the `{{ tools_path }}\powershell\modules` folder. This folder will be added to the user `PSModulePath` environment variable. The list should contain objects with **name** and **repo_url** properties, for example: `git_psmodules_tocheckout: [{ name: "WintellectPowerShell", repo_url: "https://github.com/Wintellect/WintellectPowerShell.git" }]`
psmodules_toinstall | [] | Names of PowerShell modules which should be installed from the [PowerShell Gallery](https://www.powershellgallery.com/)

Example provisioning command:

```bash
$ ansible-playbook -k -i hosts.yml playbook-debuggable-windows.yml --extra-vars "hosts=windows-local ansible_user=admin"
```

## What's in the playbook

Scripts from Inside Windows Debugging - mention that


Supports Windows 10 SDK only currently and x64 architecture

Sysinternals must precede  Process Hacker, otherwise Process Explorer will relace Process Hacker

Copy tools to diag folder if you want more tools (perfview etc.)


## Contributions

Please create an issue if you find an error in any of the configuration scripts. I will try to keep the tools up to date, but if you find any of them outdated please let me know, or create a pull request. Thank you.
