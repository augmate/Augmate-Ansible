#Ordering
--------

Run the playbooks in order of step_one, step_two, then the specific role.

###Ansible run orders and a high-level description of the Playbooks: 

----


####step_one.yml: _Secure a fresh install of Linux._

Add an admin user and group, allowing for the admin user to login via ssh and use sudo commands without typing a password.  

Set a base configuration for iptables, allowing only SSH traffic.

+ User:: Add admin user's SSH key to authorized hosts 
+ User:: Add admin to sudoers.d/ with NOPASSWD:ALL
+ Iptables / UFW:: ALLOW port 22
+ Iptables / UFW:: DENY all other 
+ SSH:: Restart SSH server


#####step_two.yml: _Common packages and users_

+ User:: Human users of the machines
+ Packages::
  * fail2ban 
  * ntp
+ Iptables / UFW:: Allow access to NTP servers and base services

#####$role.yml: _Put the base-configured server to use_







######Important things to note: 

- Where playbooks should be thought about as the base units of work, the roles are organization units to call from playbooks.  Use role dependencies to do things like calling a "nginx_nodejs" role that itself includes the base nginx role.

- Ansible runs concurrently on multiple hosts, but runs tasks serially on each host.







