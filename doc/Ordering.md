#Ordering
--------

By now, you should have read the ["Getting Started" README.md](../README.md) in this project's base directory.
 

In order to ensure that we have a standard base to all of our servers, we run a couple of _steps_ before specialization occurs.  This allows us to have some certainty that the underlying operating system for our services is acting in a uniform and predicatable manner, which in turn lowers the administrative overhead, increases security, and reduces variability in performance.

_Step one_ is concerned with facilitating remote configuration and preventing the server from unintended connections while it's being setup.  _Step two_ continues by setting up access to essential services, installing and configuring software that should be present on all of our running servers, and granting access to additional administrators.

Once these two steps are done, the server is ready to be configured for its actual purpose - providing services and doing work.  Run the playbook specific to the type of service to finish.


###Ansible run orders and a high-level description of the Playbooks: 

----

Run the playbooks in order of step_one, step_two, and then the specific role (e.g. api-server).

####step_one.yml: _Secure a fresh install of Linux._

Add an admin user and group, allowing for the admin user to login via ssh and use sudo commands without typing a password.  

Set a base configuration for iptables, allowing only SSH traffic.

This playbook is intentionally self-contained.

+ User:: Add admin user's SSH key to authorized hosts 
+ User:: Add admin to sudoers.d/ with NOPASSWD:ALL
+ Iptables / UFW:: ALLOW port 22
+ Iptables / UFW:: DENY all other 
+ SSH:: Restart SSH server

######Up for discussion: remove the ec2-user on Amazon boxes?


####step_two.yml: _Common packages and users_

Add other users that are allowed to SSH to the server, install common packages, perform tweaks to the kernel for increased performance, open the firewall up to allow for communication to core services (NTP, DNS), and remove the admin user that was created to get us to this point in step_one.

+ User:: Human users of the machines
+ Packages::
  * fail2ban 
  * ntp
+ Iptables / UFW:: Allow access to NTP servers and base services

####$role.yml: _Put the base-configured server to use_

This is the stage in which the server will become a worker machine. 

Check out the documented roles for more specific information:
#####[Documented Playbooks](./Documented_Playbooks.md)


------

######Important things to note: 

- Where playbooks should be thought about as the base units of work, the roles are organization units to call from playbooks.  Use role dependencies to do things like calling a "nginx_nodejs" role that itself includes the base nginx role.

- Ansible runs concurrently on multiple hosts, but runs tasks serially on each host.







