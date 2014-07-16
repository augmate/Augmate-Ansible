##teamcity
---

`n.b. Don't try to run this Playbook against a box with less than 512MB of RAM -- it's an unwritten minimum requirement of TeamCity.`

Ignoring this advice will lead to frustration as Linux's "OOM Killer" will terminate the TeamCity process.



####How to use:

######When spinning up a new TeamCity master:

`ansible-playbook -i inventory/development.hosts playbooks/buildbox.yml --vault-password-file .vault_pass.txt --limit buildserver-master`

To login to the web interface (port 8111 by default), look in the output of the playbook for a few lines that look like:

    TASK: [Print the last auth token in the log] **********************************
    ok: [127.0.0.1] => {
        "msg": "[2014-07-16 14:15:28,842]   INFO -  jetbrains.buildServer.STARTUP - Administrator can login from web UI using authentication token: 8121278630223467746 "
    }

The first time you spin up a master, the web interface will look for an authentication token.
The TeamCity role is just nice enough to grab such a token from the logs and output it for you.

Click 'proceed' through the prompts to create a new TeamCity database and be patient -- it's not odd for the process to take a few minutes.  When that's finished, uncheck 'Send anonymous usage statistics' and click 'Accept license agreement,' then continue.

Next, create the administrator account.  The username and password combination should be shared in a password manager to relevant users on the team.  Click 'Create account' and you're done!


######When spinning up build agents:

`ansible-playbook -i inventory/development.hosts playbooks/buildbox.yml --vault-password-file .vault_pass.txt --limit buildserver-agent`

After the Ansible playbook finishes running, the TeamCity build agent will be ready to accept jobs from the master.

Log into the master TeamCity GUI, navigate to 'agents', then the "Unauthorized" tab, and authorize your new host.


#####Troubleshooting:

"My build agent isn't trying to connect to the Build Master"

Ensure that the agent is able to communicate via the network to the build master (same subnet)?



####Little weird bits of TeamCity:

*configuration file* buildAgent/conf/buildAgent.properties has a dynamically generated parameter:
  
  - 'authorizationToken='



####Useful tips/tidbits:

To change the port used to serve the online interface:

    -TeamCity/conf/server.xml has <Connector port="8111"
    -TeamCity/buildAgent/conf/buildAgent.properties has serverUrl=
    
The memory of use can be configured: 

http://confluence.jetbrains.com/display/TCD8/Installing+and+Configuring+the+TeamCity+Server#InstallingandConfiguringtheTeamCityServer-memory

    -Xmx heap
    -XX:MaxPermSize permgen

"For initial use of TeamCity for production purposes (assuming 32 bit JVM), the minimum recommended settings are: 

	-Xmx750m 
	-XX:MaxPermSize=270m 

If slowness or OutOfMemory error occurs, please increase the settings to:

	-Xmx1200m 
	-XX:MaxPermSize=270m  

64-bit TeamCity has double this requirement.