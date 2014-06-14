api_nginx_nodejs
----------------


todo: clean this up

todo: need ability to run multiple node processes on different ports, example:

auth.api.augmate.net - port 3000

data.api.augmate.net - port 4000

web.api.augmate.net - port 5000

this mapping will reside in node configuration file: prod.config.json

Installs nginx, node.js


role dependencies: nginx, nodejs, vault


 + Sets up nginx with a sites-enabled entry that reverse proxies to nodejs
 
 + Runs nodejs on port 3000.  (I chose this port because it seems to be something of a convention in the node community)

 + adds the api to init

 + starts the api

 + does _not_ restart nginx
