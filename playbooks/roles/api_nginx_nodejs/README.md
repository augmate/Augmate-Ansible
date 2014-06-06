api_nginx_nodejs
----------------


todo: clean this up

Installs nginx, node.js


role dependencies: nginx, nodejs, vault


 + Sets up nginx with a sites-enabled entry that reverse proxies to nodejs
 
 + Runs nodejs on port 3000.  (I chose this port because it seems to be something of a convention in the node community)

 + adds the api to init

 + starts the api

 + does _not_ restart nginx