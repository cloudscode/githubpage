---
title: '阿里yum无法使用'
date: 2017-01-07 14:47:53
category: "linux"
tags: [linux,aliyun,yum]
---

## 阿里yum无法使用
### 错误信息
```
http://mirrors.aliyun.com/centos/7/os/x86_64/repodata/repomd.xml: [Errno 12] Timeout on http://mirrors.aliyun.com/centos/7/os/x86_64/repodata/repomd.xml: (28, 'Resolving timed out after 30399 milliseconds')
```
### 原因
是防火墙INPUT和OUTPUT方向全部丢弃。

### 解决方法
开启防火墙
```
chkconfig iptables on #需要重启
```
添加以下规则，并重启防火墙
```
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A OUTPUT -p tcp -m tcp -m state --state NEW --dport 80 -j ACCEPT
``` 