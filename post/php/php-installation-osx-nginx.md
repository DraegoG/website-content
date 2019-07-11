---
title: "Installing PHP and Nginx on Mac OSX"
date: 2014-08-16T13:53:51+02:00

---

> Warning: this post is old and might not reflect the current state of the art

I'll cover installing PHP on OSX via Homebrew on Nginx and PHP-FPM.

Homebrew is the best package manager for OSX and it will help keeping everything up to date.

## Install Homebrew

First [install it](http://brew.sh/) if you don't have it installed.

## Install Nginx

In the terminal type

`brew install nginx`

The default settings are:

```
Config:       /usr/local/etc/nginx/nginx.conf
Servers info: /usr/local/etc/nginx/servers/
Docroot:      /usr/local/var/www
Port:         8080
```

Add it to the Launch Agents to be started when starting up the system:

`ln -sfv /usr/local/opt/nginx/*.plist ~/Library/LaunchAgents`

Now launch it

`launchctl load ~/Library/LaunchAgents/homebrew.mxcl.nginx.plist`

All should be fine.

Add this to /usr/local/etc/nginx/nginx.conf. Make sure to change /Users/flavio/www to your sites root folder. This allows access to all the sites, which will be accessible via subfolders.


```
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;
#pid        logs/nginx.pid;

events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    include       sites-enabled/*; # load virtuals config
    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    # gzip  on;
    # gzip_disable "MSIE [1-6]\.(?!.*SV1)";

    server {
        listen       8080;
        server_name  localhost;

        #charset koi8-r;
        #access_log  logs/host.access.log  main;

        location / {
            root  /Users/flavio/www;
            try_files  $uri  $uri/  /index.php?$args ;
            index  index.php;
            #root   html;
            index  index.html index.htm;
        }

        # configure *.PHP requests

        location ~ \.php$ {
            root  /Users/flavio/www;
            try_files  $uri  $uri/  /index.php?$args ;
            index  index.html index.htm index.php;
            fastcgi_param PATH_INFO $fastcgi_path_info;
            fastcgi_param PATH_TRANSLATED $document_root$fastcgi_path_info;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;

            fastcgi_pass 127.0.0.1:9000;
            fastcgi_index index.php;
            fastcgi_split_path_info ^(.+\.php)(/.+)$;
            fastcgi_intercept_errors on;
            include fastcgi_params;
        }

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        location ~ /\.ht {
            deny  all;
        }
    }
}
```

Restart with `sudo nginx -s reload` and access `http://localhost:8080/` and you should see Nginx running. PHP sites will fail at this point.

## Install PHP 7

`brew install php70`

Add it to the Launch Agents to be started when starting up the system:

`ln -sfv /usr/local/opt/php56/*.plist ~/Library/LaunchAgents`

Now launch it

`launchctl load ~/Library/LaunchAgents/homebrew.mxcl.php71.plist`

All should be fine.

Refresh `http://localhost:8080/` and access a PHP site, PHP should be running fine!

## Install Opcache

`brew install php71-opcache`

## Install APCu

`brew install php71-apcu`


## Allow using port 80

`sudo chown root:wheel ~/Library/LaunchAgents/homebrew.mxcl.nginx.plist`

## Nginx Logs

`/usr/local/var/log/nginx/`