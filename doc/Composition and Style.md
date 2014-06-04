Composition and Style
---------------------

###On handling encrypted ('vaulted') files:

If your role requires use of an encrypted file (say, a database password or a [deploy key](https://help.github.com/articles/managing-deploy-keys)), include the `vault` role in the meta/main.yml dependencies section of the role you are writing.

e.g. 

	---
	#file: example/meta/main.yml

	dependencies:
	  - { role: vault }
 
The `vault` role ensures that the .vault_pass.txt file in the base of the ansible repo is copied to the target server.


###Playbooks

Playbooks are to be considered as the units of work in the Ansible system.  They should not do "too much" work, and instead, should be more concerned with the coordination of roles.

The ideal playbook calls a series of roles, checks that the server has the required components, and starts the service.


###Roles

Each role should be a relatively self-contained set of steps needed to bring the system to a desired state to fulfill a purpose.  

The role should not start a service.

e.g. the `nginx` role:

+ installs nginx from the package manager
+ removes the default site (the "hello world" placeholder)
+ provides the handlers needed to restart/reload/etc the service from init
+ and stops the nginx server -- but, and this is important, because the default action is to start

-----

[Back to the list of Documented Roles](./Roles.md) 