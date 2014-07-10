#Documented Playbooks
---------------------


####Note that most playbooks make extensive use of roles, which are documented on the [Roles Page](./Roles.md).


Related (and important): 

+ Working with [Ansible Vault (encrypted files)](./Vault.md)

-----

###[start](https://github.com/augmate/ansible/blob/master/playbooks/start.yml)

Do base configuration of a server - add users, SSH keys, lock down the firewall, allow admins to escalate privileges via sudo.  Further documented on the ["Ordering"](./Ordering.md) page.


Main role: None -- done via tasks.

Ports opened: 22/TCP


###[api-server](https://github.com/augmate/ansible/blob/master/playbooks/api-server.yml)

Install nodejs, git clone the [API repo](https://github.com/augmate/api), configure nginx as a reverse proxy.

Main role: [api_nginx_nodejs](https://github.com/augmate/ansible/tree/master/playbooks/roles/api_nginx_nodejs)

Ports opened: 443/TCP


###[buildbox](https://github.com/augmate/ansible/blob/master/playbooks/buildbox.yml)

Installs the Teamcity CI platform. 

http://confluence.jetbrains.com/display/TCD8/Installing+and+Configuring+the+TeamCity+Server

SubTypes:

+ Master
+ Agent 

Main role: 

Ports opened:

+ 8111
+ 9090

