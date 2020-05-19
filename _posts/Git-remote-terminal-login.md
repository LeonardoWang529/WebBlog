---
title: Git remote terminal login
date: 2020-03-28 23:22:55
tags:
- Git
categories: 'Git'
---

最近我尝试整理Git的时候，决定重新建立一个Git。于是申请了另一个账号。在push code 到新的账号Git里时。
发现一直报一个错误：大概意思是目前的用户没有权限push code到老的账号里。
我以为是 git config没有改，于是做了如下改动：
{% codeblock %}
	git config -global user.name ".."
	git config -global user.email ".."
{% endcodeblock %}
但是同样的问题依然发生。

搜索后才发现，Git在第一次永远init 的时候，输入用户名和email，会产生一个没有用户名的类似证书的东西在keychain
里可以找到。删除这个证书，在重新运行。账号转换才可以完成。

https://help.github.com/en/github/using-git/updating-credentials-from-the-osx-keychain
