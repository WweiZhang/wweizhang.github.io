---
layout: post
title: 'hello world'
date: 2018-05-04
author: wweizhang
cover: '/assets/img/hero.jpg'
tags: jekyll
---

> linux shell脚本

**刚开始写shell脚本，还不是很熟练：）**

**题目！**

![avatar](ti.png)

## 下面是题目要求检查的

* 写一个脚本实现，防止检查时操作失误，这样可以多次利用

```linux
#File Name: first.sh
#!/bin/bash
groupadd grp01
useradd -g grp01 alice
useradd -g grp01 bob

cp /etc/fstab /var/tmp/fstab
#a)
chown -R root:grp01 /var/tmp/fstab
#b)
chmod g-r,o-r,u+x /var/tmp/fstab
#acl
chown -R alice.grp01 /var/tmp/fstab
```
### 先自己通过一些命令看看以上是否正确，因为今日主要写下面的检查脚本，所以先保证题设正确
* ./fiast.sh 执行脚本
* cat /etc/passwd 查看用户是否存在了
* cd /var/tmp + ls -l 查看文件的权限

## 然后就是来检查上述的功能是否都执行正确了

```linux
#File Name: cheak.sh

if alice -u $1 >/dev/null 2>&2>&1; then
  echo "alice exists"
else
  echo "alice does not exists"
fi

if [ -d "/var/tmp" ]; then
  echo "复制失败"
fi
```
### 因为刚开始写脚本，还不太懂，今天就只检查了用户是否存在和是否复制成功，明日继续跟进！

