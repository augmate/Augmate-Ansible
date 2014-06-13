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
	

####TODO  
   
- How to use ansible's vault to work with encrypted files in a playbook/task/role.
	
----

####Related:

+ [Documented_Playbooks](Documented_Playbooks.md)

+ [Using Ansible](Using Ansible.md)
