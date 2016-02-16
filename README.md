The point of this repository is to keep a copy of our local Vagrant development VM that we can easily re-provision.

For example, to add new apache vhosts or databases, one of us should be able to edit the config.yaml file for the VM, run `vagrant provision` locally and also push the config changes up to this repo. The same changes can then be pulled and `vagrant provision` rerun on each machine we develop from.

Provided the file structure of our web projects folder on each machine is the same, this will mean config changes to our development VM are easily propagated to any machine we want and our dev environment stays more or less constant regardless where we work from.

I'll document this better as we go along.

Here's the setup instructions for Vagrant/Puphpet, stolen from here: https://puphpet.com/upload-config#help

(So there is a reference of the puphpet instructions at the time this config was generated)

##How do you pronounce PuPHPet?
The p is silent.

##What do I need to get started with PuPHPet?
There are a few pre-requisites before you can begin your virtualized journey.

First, you must install the necessary tools. They're easy to get and will only take a minute:

VirtualBox
Vagrant
Second … well, that's all you need, really.

##I downloaded the zip file (cloned this repo), now what?
Using the terminal, or cmd line, cd into your extracted directory and run $ vagrant up. This will kick-off the initial process.

Vagrant will download the box file, which can take a few minutes. It will only have to do this once, even if you create separate environments later on.

Then, it will hand control over to Puppet which will begin setting up your environment by installing required packages and configuring tools as desired.

You will then be able to ssh into your new box with $ vagrant ssh. You can also access any virtual hosts you created by editing your hosts file and creating entries for the Box IP Address and Server Name you provided during configuration (ex: 192.168.56.101 puphpet.dev www.puphpet.dev). To shut down the VM, simply run $ vagrant halt. To start it back up run $ vagrant up again. Destroy it with $ vagrant destroy.

##Further customizations with config.yaml
I have completely rewritten PuPHPet to take advantage of a built-in configuration tool for Puppet called Hiera. Simply look inside your downloaded folder and open `puppet/config.yaml`. This is the magical file that controls everything!

For example, if you want to have more OS-level packages installed (like vim, curl, git, etc) simply add more packages to server.packages. The exact same process exists for apache.modules.

To create a new Apache or Nginx vhost, simply copy/paste the one you may have created and customize to your needs.

*Attention: if you see some sections with non-sensical array keys (ex: rIreAN33ne2a) that means they have to be unique! If you copy/paste to add new settings, you must ensure you change this unique key to some other random string! Bad Things Will Happen if you don't.*

##Learn you some Vagrant
You may want to learn the basics of Vagrant CLI by going here. You really only need to learn the very basics - that is what I created this app for!

##How do I update my hosts file?
You will need to open and edit your hosts file with a text editor like notepad, sublime_text, nano, etc. The location of the hosts file varies by operation system.

Windows users could look here: c:\windows\system32\drivers\etc\hosts

Linux and Mac OSX users could look here: /etc/hosts.

Example Entry: 192.168.56.101 puphpet.dev www.puphpet.dev
