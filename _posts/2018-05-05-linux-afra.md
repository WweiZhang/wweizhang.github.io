---
layout: post
title: 'linux shell检查用户权限'
date: 2018-05-05
author: wweizhang
cover: '/assets/img/girl.jpg'
tags: linux
---

> linux shell脚本

**刚开始写shell脚本，还不是很熟练：）**

**题目！**

![avatar](/assets/img/ti.png)

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

#!/bin/bash
echo "**************************"
echo "* 选项:"
echo "* 1:检查用户及属组"
echo "* 2:检查fstab是否成功复制"
echo "* 3:检查fstab所属组"
echo "* 4:检查fstab权限"
echo "* 5:检查acl配置"
echo "**************************"
read -p "请选择：" option

case "$option" in
        1)
                group_alice=$( groups alice )
                group_bob=$( groups bob )
                echo $group_alice
                echo $group_bob 
                if [[ ${group_alice##* } = 'grp01' ]] && [[ ${group_bob##* } = 'grp01' ]]
                then
                        echo "OK!"
                else
                        echo "NO!"
                fi
        ;;
        2)
                filename=$( ls /var/tmp | grep "fstab" )
                if [[ $filename = 'fstab' ]]
                then
                        echo "/var/tmp/$filename"
                        echo "OK!"
                else
                        echo "NO!"
                fi
        ;;
        3)
                fileinf=$( ll -g /var/tmp/fstab )
                echo ${fileinf:14:5}
                if [[ ${fileinf:14:5} = 'grp01' ]]
                then
                        echo "OK!"
                else
                        echo "NO!"
                fi
        ;;
        4)
                echo "user:${fileinf:1:3} group:${fileinf:4:3} others:${fileinf:7:3}"
              if [[ ${fileinf:3:1} = 'x' ]] && [[ ${fileinf:6:1} = '-' ]] && [[ ${fileinf:9:1} = '-' ]]
                then
                        echo "OK!"
                else
                        echo "NO!"
                fi
        ;;
        5)
                fileacl_alice=$( getfacl /var/tmp/fstab | grep "alice" )
                fileacl_bob=$( getfacl /var/tmp/fstab | grep "bob" )
                echo $fileacl_alice
                echo $fileacl_bob
                if [[ ${fileacl_alice##*:} = 'rw-' ]] && [[ ${fileacl_bob##*:} = '---' ]]
                then
                        echo "OK!"
                else
                        echo "NO!"
                fi
        ;;
esac
```

