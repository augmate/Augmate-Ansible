#Ansible @ Augmate
------

##Getting started

####Pre-requisite:

- Install Python 2.7 (if not bundled with your OS)
- Install Python's 'virtualenv'
- An SSH client


####Installing Python Libs on Ubuntu


	python --version
	
Make sure your Python version is greater than > 2.7.5.  If not, stop now and get a newer version of Python.
	
	sudo apt-get python-dev
	sudo apt-get python-virtualenv

####Installing Ansible

(Optional, recommended) Activate your virtualenv.  I recommend putting your virtualenv in a directory named 'env' where you stored this repo.

e.g. 

	augmate_ansible/
		├── env

Make a virtualenv and activate it:

	virtualenv env 
	source env/bin/activate

Install Ansible:

	pip install ansible

Make sure that you received version 1.6.2 or newer:

	ansible --version
	>ansible 1.6.2


By default, Ansible uses '/etc/ansible/hosts' as its inventory of machines to configure.

You can override this from the command line by using the `-i` switch, e.g.:

	ansible all -utfisher -a "/bin/echo 'OK'" -i hosts

Or by setting an environmental variable:

	export ANSIBLE_HOSTS=~/code/ansible/inventory/production.hosts


This file has contents similar to the following:

	[webservers]
	192.168.1.14


to use a different SSH port (e.g. 2022), use `hostname.example.org:2022`.


####Add your SSH key to the remote box and get sudo

Run the `step_one.yml` playbook against your new server.  This playbook creates an admin user and starts the configuraiton process:

	ansible-playbook -i inventory/development.hosts playbooks/step_one.yml -vv -u some_user_with_sudo --ask-pass --ask-sudo-pass

Where -u is the name of the user that has root access or can _sudo_ to the _root_ user (if the user is root, remove the --ask-sudo-pass switch).  For EC2, the most likely option will `-u ec2-user --private-key=~/.ssh/my_amazon_private_key.pem `.

----

Now move on the [ordering documentation](doc/Ordering.md).
