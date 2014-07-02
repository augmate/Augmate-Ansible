# http://confluence.jetbrains.com/display/TCD8/Installing+and+Configuring+the+TeamCity+Server#InstallingandConfiguringtheTeamCityServer-memory
# -Xmx heap
# -XX:MaxPermSize permgen
# For initial use of TeamCity for production purposes (assuming 32 bit JVM),
# the minimum recommended settings are: -Xmx750m -XX:MaxPermSize=270m. If slowness or OutOfMemory error occurs, please increase the settings to -Xmx1200m -XX:MaxPermSize=270m.
#
# The maximum settings that you might ever need are (x64 JVM should be used): -Xmx4g -XX:MaxPermSize=270m.


#To change the post used:
#TeamCity/conf/server.xml has <Connector port="8111"
#TeamCity/buildAgent/conf/buildAgent.properties has serverUrl=