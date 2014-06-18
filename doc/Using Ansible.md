Using Ansible
-------------
---

####Running playbooks

To run Ansible playbooks, run the ansible-playbook command with the path of the playbook to execute, an inventory file (where to run the commands), and with the path of your [vault](./Vault.md) password file (if the playbook has encrypted content.)

	ansible-playbook -i inventory/development.hosts playbooks/api-server.yml --vault-password-file .vault_pass.txt 
	
	


