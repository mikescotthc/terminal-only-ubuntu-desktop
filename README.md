\# terminalonlydailydriver

**TERMINAL ONLY UBUNTU LAPTOP**

This is a repo of Ansible roles and playbooks to deploy an Ubuntu VM or machine to spend time entirely on the CLI. Apps to try and live in the terminal. Just to make life difficult for myself. 

If you want to run your machine as a home laptop or desktop entirely in the terminal - not a GUI in site - you can start with this.

People have done it and written articles before – the original article I read was by [Bryan Lunduke](https://www.networkworld.com/article/3085139/30-days-in-a-terminal-day-1-the-essentials.html) who set himself the challenge of running his life through the terminal for 30 days in 2016. He lasted 10 apparently. I don’t recommend doing this without another machine with the GUI to help you along! So, yeah, plenty of people more knowledgeable than me online, but my aim is to provide easy to follow instructions for someone who, like me, is getting to grips with Infra as Code whilst being geeky. Some of this will be basic, but I have found sometimes in my training, basic guides have helped me.

This repo will allow you to automate installation of all the cool tools to use the terminal for your day. My aim is to keep is updated with new apps and to streamline, eventually add automation of building the machine too, etc. 

After running the playbook, you’ll be able to do text-based web browsing (which is so satisfying), view emails, create a word processing document or presentation, export files as any compatible file type, create spreadsheets, view your favourite articles via RSS and other things that you could easily just do in the GUI without bothering with all this. But that’s less fun. 

**Prerequisites:**

This is currently tested and run using Ubuntu Server 20.04 (the current LTS edition). Get a copy of the ISO from <https://ubuntu.com/download/server> - this is fine for bare metal and on a VM using VirtualBox or [Gnome Boxes](https://help.gnome.org/users/gnome-boxes/stable/)

Download the ISO and either install on your VM or direct onto your hardware (I use [BalenaEtcher](https://www.balena.io/etcher/) for bootable ISOs). 

On current tested hardware (2014 MacBook Pro), running through the Ubuntu installer, installation failed for me with Ubuntu 21.10 - and also there were issues when Ubuntu prompted to choose to update the installer. Currently, this is all working with 20.04, using the installer provided with the original ISO install. Ensure OpenSSH is enabled on install (you’ll be prompted to enable). 

**SSH Access:**

If using a VM, ensure port 22 is open for the ansible server to contact the VM host. The following will install necessary packages and test if the VM is listening on port 22:

$ sudo apt-get install openssh-server

$ sudo apt-get install net-tools

$ systemctl start ssh.service 

$ systemctl enable ssh.service

$ netstat -tulnp | grep 22

At this point, if you’ve added the VM to the hosts file Ansible uses, you should get a positive reply from this command:
$ ansible all –m ping –k –u [username for host]

If not and you’re running the host as a VM, it’s likely it’s just settings in your hypervisor. In VirtualBox, try changing in Settings > Network from NAT (which it tends to default to) to Bridged Adaptor.

**Usage**

If you want to use the roles and playbooks as they are, ensure you define the host as ‘server01’ in your hosts file. (Default path is usually /etc/ansible/hosts). Change as you need.

Place the playbooks and roles folders inside your /etc/ansible folder, then simply run:

$ sudo ansible-playbook playbook.yml -kK –u [remoteusername] 

Or to merely do this as a dry run first:

$ sudo ansible-playbook playbook.yml -kK –u [remoteusername] --check

Currently this will install the following:

**NEOFETCH** - Visual aid to provide system and machine info

**W3M** – Great text-based internet browser

**W3M-IMG** – Images extension for W3M – means you’ll see those jpgs!

**ELINKS** – My choice of terminal-based internet browsers – very good for mouse use

**LYNX** – Old school text browser – first one I’d heard of, harder to get your head around

**ALPINE** – Only email app in the terminal that I’ve found easy to use

**WORDGRINGER** – Actual terminal word processor – like 1980s WPS on an Amiga

**PANDOC** – You'll need this to actually convert Wordgrinder files into useful formats

**VISIDATA** – Decent spreadsheet app 

**MDP** – Uses markdown language to present text all nice

**NEWSBOAT** – RSS feed reader



