---
layout: presentation
title: Continuous Deployment
permalink: /slides/deployment/
---

class: center, middle

# Deployment

Making an application live and available to its users.

---

# Agenda

1. [Overview](#overview)
1. [Production environment](#production-environment)
1. [Cloud deployments](#cloud-deployments)
1. [SSH into a Digital Ocean Droplet](#ssh-digital-ocean)
1. [Update CentOS](#update-centos)
1. [Install Node.js on CentOS](#install-node)
1. [Create a regular user account](#create-user)
1. [Deploying](#deploying)
1. [Deploying continuously](#continuous-deployment)
1. [Install nginx reverse proxy server](#install-nginx)
1. [Conclusions](#conclusions)

---

name: overview

# Overview

--

## Definitions

A few terms to clarify:

- **Delivery** is placing an app into its target environment and preparing it to run (but not actually launching it).
- **Deployment** is launching the delivered app and making it available to its end-users.
- **Continuous delivery** is automatically delivering every time a change is made to the underlying code, but waiting for a manual approval before deploying.
- **Continuous deployment** is automatically deploying every time a change is made to the underlying code.

---

template: overview

## Caveats

New releases of software, of course, must still successfully build and pass unit, integration and system tests before deployment.

---

template: overview

## Automation Pipeline

With version control, code linters, automated builds, and automated testing, continuous deployment is the natural evolution of a fully automated software development pipeline.

---

name: production-environment

# Production environment

--

## Hosting levels

There are several levels of hosting available for web applications, with many companies and services catering to each type

- Shared hosting
- Virtual Private Servers (VPS)
- Dedicated machines
- Cloud services

---

template: production-environment

## Shared hosting

With shared hosting, a developer receives an account on a web server shared by hundreds, if not thousands, of other developers.

- Historically the cheapest form of hosting
- May have restrictions in what is allowed to bee done in the account
- If one developer consumes more resources than expected, other developers may feel the effects

---

template: production-environment

## Virtual Private Servers (VPS)

With VPS, a developer receives a virtual machine running on a physical machine shared by hundreds, if not thousands, of other users.

- A step up from shared hosting
- Developers usually have discretion to do whatever they want in their virtual machine
- Each virtual machine runs in an isolated, sandboxed environment, so one account is unaffected by resourcee usage of another

---

template: production-environment

## Dedicated machine

With a dedicated machine, developers rent a single physical machine managed by the hosting company.

- A dedicated physical machine
- Admin rights to do whatever you want with it
- Software and hardware management services usually offered at additional cost.

---

name: cloud-deployments

# Cloud deployments

--

## Cloud services

A cloud is usually used to mean a grid of hundreds or thousands of physical computers all inter-networked, but presented to a developer as a single virtual machine.

Any one application may run spread across many different physical machines.

The world of cloud deployment is dominated by a few players:

- Amazon Web Services
- Microsoft Azure
- Google Cloud Platform

These are industrial-strength hosting solutions with obtuse interfaces and extensive capabilities that may be overkill and intimidating for non-specialists.

---

template: cloud-deployments

## Infrastructure-as-a-Service (IaaS)

Other providers handle much of the setup of a cloud infrastructure (compute resources, storage resources, networking interoperability, etc) without requiring the user to configure all details.

- Amazon Lightsail
- Amazon CloudFormation
- Digital Ocean
- Linode

From IaaS, developers leverage the Cloud to receive the necessary [virtual] hardware and networking abilites upon which to develop.

---

template: cloud-deployments

## Platform-as-a-Service (PaaS)

Whereas IaaS provides the hardware and networking of a cloud deployment, PaaS provide the automated install and setup of the software systems, libraries, and frameworks necessary to deploy an application.

- Heroku
- Nodejitsu
- Platform.sh
- Google App Engine

From PaaS, developers receive an environment with platform systems already setup on an appropriate cloud compute and storage inrastructure and they can simply get to work on a specific type of project development.

---

name: ssh-digital-ocean

# SSH into a Digital Ocean Droplet

--

## Concept

We will create an account with the cloud provider, Digital Ocean and set up SSH keys that allow us to log in without a password.

---

template: ssh-digital-ocean

## Create a Digital Ocean Droplet

- Create an account on Digital Ocean - use [this referral link\*](https://m.do.co/c/4d1066078eb0) for `$100` credit to use within 60 days
- Create a Droplet - select the cheapest plan with no extra options
- Choose CentOS as the operating system

- _\*Disclaimer_: I receive a referral fee if you end up paying for a Digital Ocean account. But you do not need to pay, and using this link saves you money.

- _Reminder_: You may have to enter credit card information in order to create an account. Please remember to deactivate your account once the course is over so you don't get charged.

---

template: ssh-digital-ocean
name: create-ssh-public-key

## Create a local SSH key

Create an assymetric pair of keys locally (on your own computer):

```
ssh-keygen -t rsa
```

Save the keys into the default file presented. Do not set a password.

This creates two keys in two files located within your user account's hidden `.ssh` directory:

- `id_rsa` - your private key... never share this with anyone
- `id_rsa.pub` - your public key... feel free to share this

---

template: ssh-digital-ocean

## Copy the SSH key to Digital Ocean

Locate the file with the public key you created in the previous step and copy the contents to the clipboard.

The following example shows how to do this for a user named `foobar` on a Mac.

```
cat /Users/foobar/.ssh/id_rsa.pub | pbcopy
```

Now paste this into your Digital Ocean account's `Security` / `SSH Keys` page and save.

---

template: ssh-digital-ocean
name: login-to-droplet

## Log into the Digital Ocean Droplet

With SSH keys in place on both your local machine and the Digital Ocean server, you can log in. E.g.

```
ssh root@123.456.789
```

Note: if you receive a `Permission denied` error when running `ssh`, you can try specifying the location of the private key file with the `-i` flag, e.g. `ssh -i ~/.ssh/id_rsa root@123.456.789`.

---

template: ssh-digital-ocean

## Where we are

You now have a virtual CentOS machine hosted on the cloud and can log into it from your own machine without a password.

---

name: update-centos

# Update CentOS

--

## Concept

We will update the OS and install the developer tools on the Digital Ocean Droplet

This assumes you have already [set up SSH keys](#ssh-digital-ocean) and [logged in](#login-to-droplet) to your Droplet.

---

template: update-centos

## Update system software

Update any out of date CentOS packages:

```
yum -y update
```

---

template: update-centos

## Dev tools

Install a variety of development tools:

```
yum -y groupinstall "Development Tools"
```

---

template: update-centos

## A popular text editor

A basic text editor, vim:

```
yum -y install vim
```

---

template: update-centos

## Better text editor

And a better text editor, emacs:

```
yum -y install emacs
```

---

template: update-centos

## Networking tools

Networking tools:

```
yum -y install net-tools
```

---

template: update-centos

## Install Git

Git version control:

```
yum -y install git
```

---

template: update-centos

## Where we are

You now have an up-to-date CentOS server on the Cloud with some useful development tools.

---

name: install-node

# Install Node.js on CentOS

--

## Download Node.js

Downloading of Node.js packagees is handled on CentOS by running a bash script. The following command downloads the bash script and pipes it to bash for execution:

```
curl -sL https://rpm.nodesource.com/setup_12.x | bash -
```

---

template: install-node

## Install Node

Node.js is not yet installed. To install it, run the following:
on CentOS

```
yum install -y nodejs
```

---

template: install-node

## Verify install

Now Node.js is installed. Trust but verify. Run the following to check the versions of node and npm:

```
node -v
```

```
npm -v
```

---

template: install-node

## Install an app manager

Install the popular Node.js app manager, PM2. This is used to keep a Node.js app running as a daemon and restarts it automatically if it crashes:

```
npm install -g pm2
```

---

template: install-node

## Have the app manager launch at system startup

If you desire PM2 to launch automatically when the server boots up and start any Node.js applications it has been set to manage, the following command will output a command which you can copy/paste and run:

```
pm2 startup systemd
```

---

template: install-node

## Try out a super-simple web server

Install simple http server so we can quickly serve web pages for testing:

```bash
npm install -g http-server
```

---

template: install-node

## Try loading a web page

Create a super-simple home page in a file named `index.html`:

```
echo "Hello World!" > index.html
```

Run the http-server module:

```
http-server
```

Various IP addresses of the server should be displayed. The address 127.0.0.1 is a private address that only refers to the server from the server itself - ignore it.

- Copy the next one, which is your IP address on the Internet.
- Paste the IP address into the address bar of a web browser and hit Enter.

---

template: install-node

## Where we are

You have now published a [super simple] Node.js web app on a CentOS machine living on The Cloud to The Web!

You may now stop this server and delete the `index.html` file whenever you desire.

---

name: create-user

# Create a regular user account

--

## Concept

It is best practice to only use superadministrator accounts, such as `root`, when absolutely necessary.

Doing development while logged in as a superuser could facilitate avoidable accidents and could inadvertently introduce security vulnerabilities.

We will create a "regular" user account for all developers.

---

template: create-user

## Create a new user account

Create a regular user account that you will use to set up an app:

```
adduser foobar
```

---

template: create-user

## Grant admin permissions

Add this user to the group of administrators of this machine. On CentOS, all users in the `wheel` group can use the `sudo` command to run commands as the `root` administrator user:

```
usermod -aG wheel foobar
```

---

template: create-user

## Set a password

Set a password for this user. Enter a password when prompted:

```
passwd fooobar
```

---

template: create-user

## Switch to the regular user account

Switch to the new user account:

```
sudo su - foobar
```

---

template: create-user

## Discover who you really are

```
whoami
```

---

template: create-user

## Navigate to home directory

Change to this user's home directory:

```
cd ~
```

---

template: create-user

## Set up SSH keys for the regular account

Set up the SSH keys to allow connections without passwords to this account. Only the user itself should be able to see this directory:

```
mkdir .ssh
chmod 700 .ssh
```

Create a file inside that directory:

```
touch .ssh/authorized_keys
chmod 600 .ssh/authorized_keys
```

Copy and paste the same [SSH public key](#create-ssh-public-key) from your local machine that you pasted into Digital Ocean's SSH key page into this `authorized_keys` file using a command-line text editor of your choice, such as vim or emacs.

Save the file and quit the text editor.

---

template: create-user

## Log out of the server

First return from the regular user account back to the root account:

```
exit
```

Log out of the server completely:

```
logout
```

Your command shell has now returned to your local machine.

---

template: create-user

## Log in as a regular user

SSH again to the server as the regular user account. Replace the example username and IP address below with your own:

```
ssh foobar@123.456.789
```

Note: if you receive a `Permission denied` error when running `ssh`, you can try specifying the location of the private key file with the `-i` flag, e.g. `ssh -i ~/.ssh/id_rsa foobar@123.456.789`.

---

template: create-user

## Where we are

This server is now ready for you to develop and deploy a Node.js web app.

---

name: deploying

# Deploying

--

## Concept

We can deploy a node application to the server.

---

template: deploying

## Determine your server's IP address

Determine your server's IP address using `ip addr` or `ifconfig` - from either command, you will see several IP addresses output by. Ignore the `loopback` address, which simply represents the address of your server when it talks to itself, and look for the ethernet `eth0` addresss:

```
ip addr
```

---

template: deploying

## Clone from GitHub

Clone an application from GitHub

```
git clone https://your_github_repository_url.git
```

---

template: deploying

## Start the app with PM2

Start your back-end with PM2:

```
cd your_app_directory/back-end
pm2 start npm -- start
```

--

Start your React-based front-end with PM2 (this will run the React server, which is not a proper deployment):

```
cd your_app_directory/front-end
pm2 start npm -- start
```

---

template: deploying

## Build and deploy the front-end properly

To more properly deploy a front-end built with React, you should build it and then serve it statically.

```
cd your_app_directory/front-end
npm run build # generate the HTML, CSS and Javascript into a build subdirectory
rm -rf your_app_directory/back-end/client # delete the 'client' subdirectory, if it was created earlier
cp -R ./build your_app_directory/back-end/client # copy the client-side code build to your back end's 'client' subdirectory
```

--

In your back-end main route file, create a static route that serves the front-end built code.... for example:

```
app.use("/client", express.static("client"))
```

---

template: deploying

## Verify it works

Point a web browser to your server's IP address with the port you are using to run the app. If you deployed to a static route, such as `client`, make sure to include that route in the URL.

---

name: continuous-deployment

# Deploying continuously

--

## Concept

Now that we know how to deploy a Node app, we can automate the process such that every time the `master` or `main` branch of our codebase changes, a script will update the code on the server and re-start it.

---

template: continuous-deployment

## Automation

Automation servers, such as Travis CI, Circle CI, or Jenkins, can easily trigger scripts to run when changes to the codebase are detected.

These automation tools can run a bash script that you add to your repository which...

1. connects via SSH to the web server
1. pulls the latest code from github to the server
1. re-starts the web app

---

template: continuous-deployment

## DIY

Create a bash script which automates deployment and have your automation server of choice run this script anytime the `master` or `main` branch is updated and passes tests.

---

name: install-nginx

# Install nginx reverse proxy server

--

## Concept

In order to have your web app appear when a web browser visits your server on port 80 - the default port for HTTP web requests - you will need to set up `nginx` to act as a reverse proxy "front server".

`nginx` can direct all HTTP requests at port 80 to your node.js server to any port of your choosing.

This is not necessary for continuous deployment, but puts a finishing touch to your work.

---

template: install-nginx

## Other advantages of nginx

Other advantages to using nginx are:

- easy serving of cached _static files_, rather than running dynamic scripts in response to each request
- easy setup of _https_ instead of regular http for secure/encryptic requests/responses
- easy set up of _load balancing_, where multiple instances of your server share the burden of responding to requests

---

template: install-nginx

## Install the EPEL repository

First, we must install the EPEL repository, which incluldes "extra packages for enterprise linux", including nginx:

```
sudo yum install -y epel-release
```

---

template: install-nginx

## Install nginx

Install nginx:

```
sudo yum install -y nginx
```

---

template: install-nginx

## Start nginx

Start nginx by using `systemctl` a process manager for system-related tools:

```
systemctl start nginx
```

Verify nginx starteed:

```
systemctl status nginx
```

Have nginx start automatically whenver the system reboots:

```
sudo systemctl enable nginx
```

---

template: install-nginx

## Validate the nginx is working

If you now use a web browser to navigate to `http://your_ip_address`, you should see a message that `nginx` has been installed and is running.

---

template: install-nginx

## nginx settings

By default, nginx serves files located in the `/usr/share/nginx/html` directory. You can place files in that directory to publish them. To change this server root directory, edit the configuration in `/etc/nginx/conf.d/default.conf`.

Nginx can host multiple web servers, known as Virtual Hosts. To set up virtual hosts, add new configuration files to `/etc/nginx/conf.d` - any files in this directory named `*.conf` are loaded when nginx is started.

---

template: install-nginx

## Where we are

You are now ready to configure nginx to forward requests for port 80 to another port where your node.js app is running.

To do this, you must modify nginx's settings.

---

name: conclusions

# Conclusions

---

# Conclusions

Thank you. Bye.
