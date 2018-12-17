# Project Summary:

A baseline installation of a Linux server and prepare it to host a web application. also, secure the server from a number of attack vectors, install and configure a database server, and deploy one of my existing web applications onto it. I learned how to access, secure, and perform the initial configuration of a bare-bones Linux server. and learned how to install and configure a web and database server and actually host a web application. Deploying your web applications to a publicly accessible server is the first step in getting users Properly securing your application ensures your application remains stable and that your user’s data is safe

IP address:

18.195.116.175

Grader Key attached with repository:

grader passphrase: hanyslmm

web app URL:

http://18.195.116.175.xip.io/

# User Management:

1- The SSH key submitted with the project can be used to log in as grader on the server.

2- You cannot log in as root remotely.

3- The grader user can run commands using sudo to inspect files that are readable only by root.

# Security:

1- Only allow connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).

2- Key-based SSH authentication is enforced.

3- All system packages have been updated to most recent versions.

sudo apt-get update --> updates the list of available packages and their versions,
but it does not install or upgrade any packages.

sudo apt-get upgrade --> actually installs newer versions of the packages you have.
After updating the lists, the package manager knows about available updates
for the software you have installed. This is why we first update.

4- SSH is hosted on port 2200.

# Application Functionality:

Flask application running in docker container and port mapping 80:5000 to open app through browser default port.

Steps to Configure Server on AWS:

1- Start a new Ubuntu Linux server instance on Amazon Lightsail.

2- Follow the instructions provided to SSH into your server.

# Secure your server:

1- Update all currently installed packages.

2- Change the SSH port from 22 to 2200.

3- Make sure to configure the Lightsail firewall to allow it.

4- Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).

Warning: When changing the SSH port, make sure that the firewall is open for port 2200 first, so that you don't lock yourself out of the server. When you change the SSH port, the Lightsail instance will no longer be accessible through the web app 'Connect using SSH' button. The button assumes the default port is being used. There are instructions on the same page for connecting from your terminal to the instance. Connect using those instructions and then follow the rest of the steps.

5- Create a new user account named grader:

Give grader the permission to sudo: cp /etc/sudoers/ cp /etc/sudoers.d/90-cloud-init-users /etc/sudoers.d/grader; and edit it with garder username

6- Create an SSH key pair for grader using the ssh-keygen tool.

### Then Prepare to deploy the project.

7- Configure the local timezone to UTC:

timedatectl list-timezones
timedatectl set-timezone UTC

8- Install packages to allow apt to use a repository over HTTPS:
$ sudo apt-get install 
apt-transport-https 
ca-certificates 
curl 
software-properties-common

9- Add Docker’s official GPG key:
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - 

10- Verify that you now have the key with the fingerprint: 
sudo apt-key fingerprint 0EBFCD88

11- Use the following command to set up the stable repository. You always need the stable repository, even if you want to install builds from the edge or test repositories as well. 

sudo add-apt-repository 
"deb [arch=amd64] https://download.docker.com/linux/ubuntu 
$(lsb_release -cs) 
stable"

12- Install the latest version of Docker CE, or go to the next step to install a specific version:
$ sudo apt-get install docker-ce

13- Pull Item Catalog docker image:
sudo docker pull hanyslmm/crud_webapp:AWS

14- run a container using a following command:
sudo docker run -it -p 80:5000 --name itemcatalog --hostname server hanyslmm/crud_webapp:AWS python3 project.py

server now up and you can run check.

### How to write good REDME File:

https://classroom.udacity.com/courses/ud777

https://changelog.com/posts/a-beginners-guide-to-creating-a-readme

### Disable remote root login:

https://www.tecmint.com/disable-root-login-in-linux/

### Difference between update and upgrade:

https://askubuntu.com/questions/94102/what-is-the-difference-between-apt-get-update-and-upgrade

### vim shortcuts:

https://www.maketecheasier.com/vim-keyboard-shortcuts-cheatsheet/
