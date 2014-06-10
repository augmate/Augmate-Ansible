#Ordering
--------

By now, you should have read the ["Getting Started" README.md](../README.md) in this project's base directory.
 

In order to ensure that we have a standard base to all of our servers, we run a _start_ playbook before specialization occurs.  This allows us to have some certainty that the underlying operating system for our services is acting in a uniform and predicatable manner, which in turn lowers the administrative overhead, increases security, and reduces variability in performance.

_Start_ is concerned with facilitating remote configuration, preventing the server from unintended connections while it's being setup, allowing access to essential services, installing and configuring software that should be present on all of our running servers, and granting access to additional administrators.

Once this step is done, the server is ready to be configured for its actual purpose - providing services and doing work.  Run the playbook specific to the type of service to finish.


###Ansible run orders and a high-level description of the Playbooks: 

----

Run the playbooks in order of `start.yml` and then the specific role (e.g. `api-server.yml`).

####start.yml: _Secure a fresh install of Linux, install common packages, and add users_

Add other users that are allowed to SSH to the server, install common packages, perform tweaks to the kernel for increased performance, open the firewall up to allow for communication to core services (NTP, DNS), and remove the admin user that was created to get us to this point in step_one.

Set a base configuration for iptables, allowing only SSH traffic.

+ User:: Human users of the machines
+ User:: Allow admin users to sudo without using a password. (sudoers.d/ with NOPASSWD:ALL)
+ User:: Add users' SSH keys to authorized hosts 
+ Group:: Add an admin group for users
+ Iptables / UFW:: ALLOW port 22
+ Iptables / UFW:: Allow access to NTP servers and base services
+ Iptables / UFW:: DENY all other 
+ SSH:: Restart SSH server
+ Packages::
  * fail2ban 
  * ntp

######Up for discussion: remove the ec2-user on Amazon boxes?



####$role.yml: _Put the base-configured server to use_

This is the stage in which the server will become a worker machine. 

Check out the documented roles for more specific information:
#####[Documented Playbooks](./Documented_Playbooks.md)


------

######Important things to note: 

- Where playbooks should be thought about as the base units of work, the roles are organization units to call from playbooks.  Use role dependencies to do things like calling a "nginx_nodejs" role that itself includes the base nginx role.

- Ansible runs concurrently on multiple hosts, but runs tasks serially on each host.







