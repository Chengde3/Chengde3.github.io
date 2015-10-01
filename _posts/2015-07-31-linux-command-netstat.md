---
layout: post
title: Linux命令之netstat
date: 2015-07-31
categories: Linux
tags: linux netstat
---

之前遇到过几次这个命令，今天总结一下，方便下次使用

## 1. 概述

netstat可以用来显示如下内容：

- 网络连接
- 路由表
- 接口统计
- 伪连接
- 组播成员。

## 2. 常用参数

一般使用如下命令即可：

netstat -anp

- -a(all):显示所有内容
- -t(tcp):仅显示tcp相关内容
- -u(udp):仅显示udp相关内容
- -n(numeric）:直接显示ip地址以及端口，不解析
- -l(listen):仅列出Listen（监听）的服务
- -p(pid):显示出socket所属的进程PID以及进程名字
- -r:显示路由信息，路由表
- -e:显示扩展信息，例如uid等
- -s:按各个协议进行统计
- -c:每隔一个固定时间，执行该netstat命令

注：加参数'-n'会将应用程序转为端口显示，即数字格式的地址，如：nfs->2049,ftp->21,

## 3. ss命令和ip命令

看到这篇[文章](http://roclinux.cn/?p=2418)说netstat官方以及不再更新了，已经被ss命令和ip命令所取代。建议使用ss和ip命令。但是自己man netstat并没有发现类似的说明，姑且认同吧。暂时没有打算仔细学习ss和ip命令，盗用作者的一张图吧。

![netstat&&ip&&ss](../image/netstat_subsititute.jpg)

## 4. 其它

一般使用netstat查看端口后会有关闭该端口的需求，有一下两种方法。
1) 通过iptables工具将端口关闭
{% highlight sh %}
sudo iptables -A INPUT -p tcp --dport $PORT -j DROP
sudo iptables -A OUTPUT -p tcp --dport $PORT -j DROP
{% endhighlight sh %}

2) 关掉对应的应用程序
{% highlight sh %}
kill -9 PID(PID是进程号)
{% endhighlight sh %}

例如关闭22号端口：
{% highlight sh %}
netstat -anp | grep :22
//显示
tcp 0  0 0.0.0.0:22    0.0.0.0:*  LISTEN  988/sshd
kill -9 998
{% endhighlight sh %}

注：一些端口通过netstat查不出来，可以使用如下方法：
{% highlight sh %}
sudo nmap -sT -O localhost
{% endhighlight sh %}

## 5. 参考文献

- [《和netstat说再见》-linux命令五分钟系列之三十](http://roclinux.cn/?p=2418)
- [linux netstat 命令详——查看端口使用情况](http://zyjustin9.iteye.com/blog/2017213)
- [linux netstat 命令详解](http://www.cnblogs.com/azheng007/p/3159320.html)
- [每天一个linux命令（56）：netstat命令](http://www.cnblogs.com/peida/archive/2013/03/08/2949194.html)
- [Linux查看端口使用状态、关闭端口方法](http://blog.csdn.net/wudiyi815/article/details/7473097)
- [Linux端口状态查看、启用和关闭](http://blog.csdn.net/zqj6893/article/details/18001689)