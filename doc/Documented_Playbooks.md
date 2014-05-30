#Documented Playbooks
---------------------
##(work in progress)



####Note that most playbooks make extensive use of roles, which are documented on the [Roles Page](./Roles.md).

-----

###step_one / step_two

step_one and step_two can be thought of as the "base layers" and are documented on the ["Ordering"](./Ordering.md) page.

--

###api-server

Brings an API server online.

Install packages:

+ nodejs 
+ nginx

Roles: 

+ nginx_api_nodejs : configure nginx for serving the nodejs based API.
    - depends on role `nginx`

+ nodejs 

Ports opened


###buildbox

Installs the Teamcity CI platform. 

http://confluence.jetbrains.com/display/TCD8/Installing+and+Configuring+the+TeamCity+Server

Tags:

+ Master
+ Agent 

Roles: 


Ports opened



###website 

Configures a webserver with the assets needed to serve [Augmate.com](http://augmate.com).


nodejs
static assets (html, js, css)