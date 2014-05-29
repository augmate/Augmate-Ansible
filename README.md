##Ansible @ Augmate 
------

####Pre-requisite: 

- Install Python 2.7 (if not bundled with your OS)
- Install Python's 'virtualenv'
- An SSH client

####Installing Ansible

Activate your virtualenv.  

Install Ansible: 

	pip install ansible
	
	
By default, Ansible uses '/etc/ansible/hosts' as its inventory of machines to configure.

You can override this from the command line by using the `-i` switch, e.g.:

	ansible all -utfisher -a "/bin/echo 'OK'" -i hosts
	
Or by setting an environmental variable:

	export ANSIBLE_HOSTS=~/code/ansible/inventory/production.hosts


This file has contents similar to the following:

	[webservers]
	192.168.1.14


to use a different SSH port (e.g. 2022), use `hostname.example.org:2022`.


##Add your SSH key to the remote box and get sudo 

Run the `step_one.yml` playbook against the new 

	ansible-playbook -i inventory/development.hosts playbooks/step_zero.yml -u root --ask-pass


----



Now move on the ordering documentation.