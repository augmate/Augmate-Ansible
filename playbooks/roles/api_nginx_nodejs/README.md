api_nginx_nodejs
----------------

Installs nginx, node.js

role dependencies: nginx, nodejs, vault


 + Sets up nginx with a sites-enabled entry that reverse proxies to nodejs
 
 + Runs nodejs on port 3000

 + adds the api to init

 + starts the api

 + does _not_ restart nginx
