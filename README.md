Project Summary:

A baseline installation of a Linux server and prepare it to host a web application. also, secure the server from a number of attack vectors, install and configure a database server, and deploy one of my existing web applications onto it. I learned how to access, secure, and perform the initial configuration of a bare-bones Linux server. and learned how to install and configure a web and database server and actually host a web application. Deploying your web applications to a publicly accessible server is the first step in getting users Properly securing your application ensures your application remains stable and that your user’s data is safe

IP address:

18.195.116.175

Grader Key attached with repository:

grader passphrase: hansylmm

web app URL:

http://18.195.116.175.xip.io/

User Management:

1- The SSH key submitted with the project can be used to log in as grader on the server.

2- You cannot log in as root remotely.

3- The grader user can run commands using sudo to inspect files that are readable only by root.

Security:

1- Only allow connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).

2- Key-based SSH authentication is enforced.

3- All system packages have been updated to most recent versions.

4- SSH is hosted on port 2200.

Application Functionality:

Flask application running in docker container and port mapping 80:5000 to open app through browser default port.

Steps to Configure Server on AWS:

Start a new Ubuntu Linux server instance on Amazon Lightsail.

Follow the instructions provided to SSH into your server. Secure your server:

Update all currently installed packages.

Change the SSH port from 22 to 2200. Make sure to configure the Lightsail firewall to allow it.

Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).

Warning: When changing the SSH port, make sure that the firewall is open for port 2200 first, so that you don't lock yourself out of the server. When you change the SSH port, the Lightsail instance will no longer be accessible through the web app 'Connect using SSH' button. The button assumes the default port is being used. There are instructions on the same page for connecting from your terminal to the instance. Connect using those instructions and then follow the rest of the steps.

Create a new user account named grader:

Give grader the permission to sudo: cp /etc/sudoers/ cp /etc/sudoers.d/90-cloud-init-users /etc/sudoers.d/grader; and edit it with garder username

Create an SSH key pair for grader using the ssh-keygen tool. Prepare to deploy your project.

Configure the local timezone to UTC:

timedatectl list-timezones
timedatectl set-timezone UTC

Install packages to allow apt to use a repository over HTTPS:
$ sudo apt-get install 
apt-transport-https 
ca-certificates 
curl 
software-properties-common

Add Docker’s official GPG key:
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - 

Verify that you now have the key with the fingerprint: 
sudo apt-key fingerprint 0EBFCD88

Use the following command to set up the stable repository. You always need the stable repository, even if you want to install builds from the edge or test repositories as well. 

sudo add-apt-repository 
"deb [arch=amd64] https://download.docker.com/linux/ubuntu 
$(lsb_release -cs) 
stable"

Install the latest version of Docker CE, or go to the next step to install a specific version:
$ sudo apt-get install docker-ce

Pull Item Catalog docker image:
sudo docker pull hanyslmm/crud_webapp:AWS

run a container using a following command:
sudo docker run -it -p 80:5000 --name itemcatalog --hostname server hanyslmm/crud_webapp:AWS python3 project.py

server now up and you can run check.
