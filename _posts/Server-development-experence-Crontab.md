---
title: Server development Experience Crontab
date: 2019-02-26 06:49:36
tags:
- server
categories: 'Web Server'
---

When I was writing a crontab today on linux system, the crontab never runned. Although I have follow the rule of crontab.

{% codeblock lang:objc %}
* * * * * python3 checkrunning.py
{% endcodeblock %}

At first I thought it was the location of the file and python is not in current location. So I used absolute path, but the crontab is still not running.

After research I understand the script is at another location. In order to use it in current location. We have cd to current in the crontab first. and use && to connect two command. This time the crontab is start successfully.

{% codeblock lang:objc %}
* * * * * cd /path/to/current/location && /path/to/python3 /path/to/checkrunning.py &
{% endcodeblock %}
