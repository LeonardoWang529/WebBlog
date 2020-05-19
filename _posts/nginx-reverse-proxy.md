---
title: Nginx Reverse Proxy
date: 2020-05-19 03:27:20
tags: server
categories: 'Web Server'
---

Nginx has the ability of reverse proxy.
Reverse proxy means, different URL requests can be sent to same IP address.
The IP address will received request with URL and sent to different services

Reverse proxy allows one server take multiple servers works.
Reuse the same server code from different URL.
Using the same port number(80) with different server_name.
Enables load balancing and failover

The reverse proxy tasks can be implement in /etc/nginx
Instead of putting server{} in nginx.conf files
Nginx creates a folder called sites-enabled.
In the sites-enabled file:

{% codeblock %}
server {
  server_name xxxx.com;

  location / {
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";

      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header Host $http_host;
      proxy_set_header X-NginX-Proxy true;
      proxy_pass    http://127.0.0.1:5000/;
    }
}
{% endcodeblock %}

We can create multiple servers like this, either point to same server_name but different port number. Or different server_name, but the server_name has to be valid(ping able).

The proxy_pass can point to the code that is current running in the back.
Here, we are point to local ip 5000 port, which has an nodeJs running under PM2 daemon process.
