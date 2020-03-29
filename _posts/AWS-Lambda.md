---
title: AWS Lambda
date: 2017-11-30 00:57:54
tags:
- AWS
- Lambda
categories: "Coding"
---

AWS Lambda is a web servers that allow you to run code without thinking about servers.
AWS Lambda has two major advantages:

1. AWS Lambda is scalable , Apache on instanse have its limitation. when the clint requires is huge. Apach on instance can not handle. We need to user loadbalancer to handle some issue. When work with Lambda, all this is taking cared by AWS itself, it is more easy.

2. AWS Lambda is also taking care the Rest Call, when we using http://example.com/getName?id = 1000, we have a full RestFul setup on the back. After we upload all our function in ot Lambda, we can dirctly call it using the way that Lambda setup, Rest enviorment is no longer require. Save a lot of time to do maintains.

For more detail, I will keep upload it, when I start to use it.
