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

Go to the folder you wish to save your project. And git clone this project. You will have the vagrantfile directly onto your folder ready to be launched. my vagrant file is a little bit different than the sample one in the Docker section. I added some stuff to be able to install certain fonctionalities.   

# 4. Start the vm 
Go to the terminal and go to the directory where your vagrantfile is located (cd /../../path/) and do:

`vagrant up --provider=docker`

**You only need to specify the provider during the first time. After that you can just use `vagrant up` . If you do not specify during the first time to use Docker, they will use the default, which is VirtualBox, so you will probably will get an error.**


You should not get any errors and your image should be created and be running at this point. To check go to docker and see if a new image was created and if it is running. Remember if your docker is offline, vagrant will not be able to launch the VM, so if you get a problem with docker deamon is probably because of that. 

If everything is okay, in the same terminal :

`vagrant ssh`

And just like that we have acces to the terminal of the VM! Congrants!

# 5 Install necessary packages

Lets download some useful packages : 

`sudo apt-get update`
`sudo apt-get install nano`
`sudo apt-get install iproute2`
`sudo apt-get install ufw`
`sudo apt-get install -y inetutils-ping`

Voila, we should have the basics to begin using pour VM as installing our programs. 

# 6. nginx

I am installing nginx to get a a web server and access it though our actual host machine (our computer instead of inside the VM). In the vagrant file I specified a private network and technically we would be able to acces this IP address through the Host machine but I was not able. The solution for me was to foward a port. 

This is what we have on our VagrantFile:

` config.vm.network "private_network", ip: "192.168.56.10"
 config.vm.network "forwarded_port", id: "nginx", host: 8080, guest: 80`

The foward port will allows us to access through the port specified : 8080. (localhost:8080)
Since we are gonna use the port 8080 to communicate with our VM, make sure any other application is using this port. 

So now lets install nginx and add some configuration :

 ```
 sudo apt-get install ngixt
 sudo service nginx start.
 sudo ufw allow 80/tcp
```
If it is working you should be able to see from :
`sudo service nginx status`

If it is running we are good!. 

Now go to your browser (chrome, safari whatever) and put http://localhost:8080/ -> You should be seing the nginx front page. Congrats!
 


