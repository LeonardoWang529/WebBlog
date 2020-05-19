---
title: Web Basic Structure
date: 2020-05-19 07:10:57
tags: server
categories: 'Web Server'
---

In my previous post Nginx Reverse Proxy, I have talked about how different URL can point to same server machine but different services. In this article I will talk about how to get different URLs.

The URL works like this:
You typed a URL, Domain Name Service(DNS) will being ask what is the ip address related to this URL.
than you will be router to the ip address machine. At this point, Nginx on this machine received the message, it sees the request is coming from which URL, and sent the request to the service that is bind with the URL.

In reality, DNS is not free. There are couple big company runs this service such as Godaddy. User can pick a URL and give it to Godaddy, User also need to give a ip address. Godaddy will store ip address with this URL. In my Case, I am using DigitalOcean, which also do DNS. So new URL Nameservers will be set to DigitalOcean nameservers.
So when Godaddy is been asked about the IP address of this URL. Godaddy will say, GO ASK DigitalOcean. That is why, we also need set up an ip and URL pair in DigitalOcean.

Till now all of this steps are preformed in the 'outer net'. Every URL must have a DNS who knows what IP address it is bind with. If outer net get a URL but no provider knows the Ip address, Nothing will shows up. The first question should be ask is: who did this URL's Domain Name Service in outer net. Nginx only do 'inner net' routing: tell which client service should this URL going to in server machine.

If you want to check if a URL is valid, you can ping the URL
