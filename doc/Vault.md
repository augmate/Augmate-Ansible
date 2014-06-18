Working with Ansible Vault
---------------------------


Running Playbooks with "Vaulted" files:


Interactively:

	ansible-playbook site.yml --ask-vault-pass


Non-interactively (needed for deploying servers):

	ansible-playbook site.yml --vault-password-file ~/.vault_pass.txt

There's going to need to be some cloak-and-dagger component to getting this working (we can't store the vault pass in the repo).  Perhaps the server build-script can do this so we only have to manually place the file once. 


###Encrypting files

	ansible-vault encrypt foo.yml

###Decrypting files

	ansible-vault decrypt foo.yml

###Editing encrypted files

	ansible-vault edit foo.yml
	
###Using vault when writing Tasks

Put your secret information into a `vars` file, reference that `vars` file from your `task`, and encrypt the whole `vars` file using `ansible-vault encrypt`.

Let's use an example: You're writing an Ansible role and want to encrypt the spoiler for the movie [Aliens](http://www.imdb.com/title/tt0090605/).

Your Ansible role should have the following structure similar to the following:

	roles/aliens
		├── tasks
		│   └── main.yml
		└── vars
    		    └── spoilers.yml


First, put your spoiler text in a roles/aliens/vars/spoilers.yml:

	---
	spoiler_text: | 
	  people run into some space aliens
	  and they end up fighting them

(Note the pipe, followed by the new line with text indented by two spaces.  This allows you to easily put multi-line text into a variable.)

Then, reference your `spoiler_text` variable in your task:

	---
	- include_vars: spoilers.yml
	
	- name: Put the spoiler text in the tmp directory on the remote server.
	  copy:
	    content="{{spoiler_text}}"
	    dest=/tmp/spoiler_text.txt
    	
    	
Encrypt your spoilers file using your vault password file on the command line:

	$ ansible-vault encrypt roles/aliens/vars/spoilers.yml --vault-password-file ~/.vault_pass.txt
	Encryption successful
	
You can now safely put this file in your source control without spoiling the movie for everyone.

	$ head -n3 aliens/vars/spoilers.yml
	$ANSIBLE_VAULT;1.1;AES256
	61616366326131636131323230613333356361333737356566646133343062623061313931666462
	3933316533346664393430643963646533663737343434320a613862353665663862393939383336
	...

Then, given a playbook that looks like:

	---
	# file: movies.yml
	- hosts: all
	
	  roles:
	    - { role: aliens }
	    
You can now run this against your server:


	$ ansible-playbook -i inventory/development.hosts playbooks/movies.yml --vault-password-file ~/.vault_pass.txt

That's it!  Hop on the server and you can see that the decrypted content is there on disk:

	remote_server$ cat /tmp/spoiler_text.txt 
	people run into some space aliens
	and they end up fighting them
	

----

####Related:

+ [Documented_Playbooks](Documented_Playbooks.md)

+ [Using Ansible](Using Ansible.md)
