---
title: Server development Experience NGINX
date: 2019-03-09 05:49:13
tags:
- server
categories: 'Web Server'
---

In the past couple days, I am developing a full website, from front to end.
when I was working on Restful api, I notice that the url call such like http://tamedogisnotdog.com/external/RestServer/v1/test
although index.php for rest is in v1. but the server treated test as a sub folder of v1 instead of rest call.

What should I do?
So it turns out that we have to set some value in nginx.
path: /etc/nginx/nginx.conf
{% codeblock %}
    server {
        server_name tamedogisnotdog.com;
        root /var/www/html/snowtools;

	# redirct all the call after v1 to index.php under v1
        rewrite ^/external/RestServer/v1/(.*)$ /external/RestServer/v1/index.php;      

	# force php to run php as a script, instead of txt file
	location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.0-fpm.sock;
        }
    }
{% endcodeblock %}
I added this in http {}
and restart the nginx with nginx -s stop and nginx.
Then the problem is sloved.

So snippets is belong to nginx: https://www.nginx.com/resources/wiki/start/topics/examples/fastcgiexample/
include 类似于 java 的 import pacage.
fastcig pass is also belong to nginx: use fastcig pass to process some data from  php fpm ，
unix:/run/php/php7.0-fpm.sock is belong to php

in nginx fastcgi pass is a commend  directive，like

{% codeblock %}
<section> {

  <directive> <parameters>;

}
{% endcodeblock %}

Reference:
https://stackoverflow.com/questions/2936260/what-language-are-nginx-conf-files
