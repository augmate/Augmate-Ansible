##teamcity


####Don't try to run this Playbook against a box with less than 512MB of RAM -- it's an unwritten minimum requirement of TeamCity.

Ignoring this advice will lead to frustration as Linux's "OOM Killer" will terminate the TeamCity process.

####Other notes about memory:

http://confluence.jetbrains.com/display/TCD8/Installing+and+Configuring+the+TeamCity+Server#InstallingandConfiguringtheTeamCityServer-memory

    -Xmx heap
    -XX:MaxPermSize permgen

"For initial use of TeamCity for production purposes (assuming 32 bit JVM), the minimum recommended settings are: -Xmx750m -XX:MaxPermSize=270m. If slowness or OutOfMemory error occurs, please increase the settings to -Xmx1200m -XX:MaxPermSize=270m."  64-bit TeamCity has double this requirement.

- The maximum settings that you might ever need are (x64 JVM should be used): -Xmx4g -XX:MaxPermSize=270m.


####To change the port used to serve the online interface:

    -TeamCity/conf/server.xml has <Connector port="8111"
    -TeamCity/buildAgent/conf/buildAgent.properties has serverUrl=


####Notes on scaling:

Set up an external database (such as MySQL), then set the external database location in the config file.