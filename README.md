# NGINX-NODEJS

This image provides an easy way of serving a web app that also needs Node.js for building (by running webpack, compiling styles...).

Node.js is intended for building the app solely. If what you try to accomplish is a nginx proxy that points to a Node.js server then my advice is to not use this image. Instead follow the "one container -> one process" rule and run the proxy and the Node.js server in separated containers.

The image also aims for just nginx serving. If you need other features like git or ssmtp in the same image I'd head to other options like codekoalas/nginx-node.


## NGINX version

The nginx used by this image comes from the official repositories of Debian 8 "Jessie", as the base Node.js images used are the jessie versions.


## Configuration environment variables

The default configuration of the site is the same that you'd find in the default configuration that comes with the nginx install. This image provides a way of changing some of the values of that conf using the next environment variables:
 - NGINX_ROOT: root directory for requests (default: /var/www/html)
 - NGINX_PORT: port for listening to requests (default: 80)
 - NGINX_SERVER\_NAME: name of the virtual server (default: \_)
 - NGINX_INDEX: list of files (space separated) used as index (default: "index index.html index.htm index.nginx-debian.html")


## Using custom conf file

If you'd like to use your own configuration file (very likely) but still use the variable substitution you can specify the conf file by setting the environment variable NGINX_SITE_FILE.

Keep in mind that the image will try to substitute every env variable, which means that you can use the configuration variables stated above and your own variables.

Examples:
````
docker run -v ./my.conf:/my.conf -e NGINX_SITE_FILE=/my.conf -e NGINX_INDEX="index.html" -e MY_OWN_VAR=foo emud/nginx-nodejs
````

````
#Dockerfile
FROM emud/nginx-nodejs

COPY ./my.conf /my.conf

ENV NGINX_SITE_FILE /my.conf
ENV MY_OWN_VAR foo
````


## Disabling environment substitution

If you don't want the environment substitution you just have to set the environment variable REPLACE_DEFAULT to false.
