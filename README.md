# MacM1VirtualMachine
If you need to install a Linux Virtual Machine using Vagrant on your Mac M1/M2 and do not want to pay for Parallels, I have the solution. Follow the tutorial

# Problem 

Today, the programs for launching a VM machine in a M1/M2 mac is : 
 * Parallels : It can cost anything from $50-$150 dollars (if you can afford it go ahead).
 * UTM : Free but does not let you integrate with Vagrant.
 * VmWare : They have a free version but at least for me, I ran into a lot of errors while trying to launch the VM. 
 
 # Solution
 
 ## Docker
 Docker allows us to launch a virtual machine and thanks to Rofrano, (https://hub.docker.com/r/rofrano/vagrant-provider) that allows us to connect it to Vagrant. 
 
 Now, there are some details that you guys need to pay attention while creating and setting up the machine. I will show how to do for Ubuntu 22.2 (Jammy). 
 
I will show how you can successfully install : nginx, java, python, r and git. 

# 1. Download Docker for desktop

https://www.docker.com/products/docker-desktop/

I recommend installing Docker for desktop because it allows us to see the image (in our case the VM) being created and is more intuitive. 
Once you install it, just launch the app and make sure it says "Docker Desktop is running".

# 2. Download Vagrant

Vagrant is a powerful program that allows us to create/modify/destroy virtual machines with almost no effort. You only need to create a file (VagrantFile) and it will do whatever you tell it to do. 

On your terminal, insert the following command line (assuming you have homebrew):

`brew install --cask vagrant`

# 3. Git Clone

Go to the folder you wish to save your project. And git clone this project. You will have the vagrantfile directly onto your folder ready to be launched. 

# 4. Start the vm 
Go to the terminal and go to the directory where your vagrantfile is located (cd /../../path/) and do:

`vagrant up --provider=docker`

**You only need to specify the provider during the first time. After that you can just use `vagrant up` . If you do not specify during the first time to use Docker, they will use the default, which is VirtualBox, so you will probably will get an error.**


You should not get any errors and your image should be created and be running at this point. To check go to docker and see if a new image was created and if it is running. Remember if your docker is offline, vagrant will not be able to launch the VM, so if you get a problem with docker deamon is probably because of that. 

If everything is okay, in the same terminal :

`vagrant ssh`

And just like that we have acces to the terminal of the VM! Congrants!


