# fedora-workstation-ansible #

This is my provisioner for the Fedora 29. 

### Usage: ###

1. Clone this repo
1. Install prerequisites on destination box: `dnf -y install ansible sudo python-dnf libselinux-python`
1. Create entry for your user in **/etc/sudoers.d/user**
1. Enter proper **ansible_ssh_host** and **ansible_ssh_user** in **hosts** file
1. Make sure it works: `ansible -m ping <your_host>`
1. Rollout: `ansible-playbook master.yml`

Of course you may install just a specified part of the
whole installation by using tags. List available tags
with:

`$ ansible-playbook master.yml --list-tags`

 And install specified part with:

`$ ansible-playbook master.yml --tags dropbox,virtualbox`

If you want to only update packages (like `dnf update -y` simply run:

`$ ansible-playbook master.yml --tags pkgs,update --skip-tags install`

### Managing multiple desktops ###

I use this repository in order to manage 5+ laptops. There are two methods to achieve this
multi - desktop configuration:

1. First is to keep every workstation configuration in different branch. This way every workstation
   has its own **master.yml** and **hosts** file. Downside is the need for keeping branches in sync
   (which is a basic merge so it's not a rocket science).
1. Second is to keep every workstation provisioner in different playbook (e.g. in **plays** directory).
   In this scenario you keep all hosts configuration in one **hosts** file.

