# Bash setup script for Ubuntu servers
[![Build Status](https://travis-ci.org/jasonheecs/ubuntu-server-setup.svg?branch=master)](https://travis-ci.org/jasonheecs/ubuntu-server-setup)

This is a setup script to automate the setup and provisioning of Ubuntu servers. It does the following:
* Adds or updates a user account with sudo access
* Adds a public ssh key for the new user account
* Disables password authentication to the server
* Deny root login to the server
* Setup Uncomplicated Firewall (allow SSH, port 80 and 443)
* Setup Fail2Ban (default config)
* Setup the timezone for the server (Default to "Europe/Rome")
* Install Network Time Protocol

# Installation
SSH into your server and install git if it is not installed:
```bash
sudo apt-get update
sudo apt-get install git
```

Clone this repository into your home directory:
```bash
cd ~
git clone https://github.com/jasonheecs/ubuntu-server-setup.git
```

Run the setup script
```bash
cd ubuntu-server-setup
bash setup.sh
```

# Setup prompts
When the setup script is run, you will be prompted to enter the username of the new user account. 

Following that, you will then be prompted to add a public ssh key (which should be from your local machine) for the new account. To generate an ssh key from your local machine:
```bash
ssh-keygen -t ed25519 -a 200 -C "user@server" -f ~/.ssh/user_server_ed25519
cat ~/.ssh/user_server_ed25519.pub
```

Finally, you will be prompted to specify a [timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) for the server. 

# Manual Setup to automate
- [ ] Install nginx (tutorial)[https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04]
- [ ] Configuring Fail2Ban to Monitor Nginx Logs [tutorial](https://www.digitalocean.com/community/tutorials/how-to-protect-an-nginx-server-with-fail2ban-on-ubuntu-20-04#step-2-configuring-fail2ban-to-monitor-nginx-logs)
- [ ] Change SSH port (from 22 to another)
- [ ] Create SSH key and add it to github secrets, to use it in github actions: [tutorial](https://dev.to/knowbee/how-to-setup-continuous-deployment-of-a-website-on-a-vps-using-github-actions-54im)


# Supported versions
This setup script has been tested against Ubuntu 14.04, Ubuntu 16.04, Ubuntu 18.04, Ubuntu 20.04 and Ubuntu 22.04.

# Running tests
Tests are run against a set of Vagrant VMs. To run the tests, run the following in the project's directory:  
`./tests/tests.sh`
