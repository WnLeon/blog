---
layout: post
title: "Centos7下yum安装mysql5.7 "
categories: home
tags: "mysql "
excerpt_separator: <!--more-->
--- 


<!--more-->
centos7 yum安装mysql5.7

## 官方源：
```
wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
yum -y install mysql57-community-release-el7-10.noarch.rpm
yum -y install mysql-community-server
```


## 国内阿里源：
```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
yum makecache
yum update -y

wget http://mirrors.ustc.edu.cn/mysql-ftp/Downloads/MySQL-5.7/mysql-community-server-5.7.30-1.el7.x86_64.rpm
wget http://mirrors.ustc.edu.cn/mysql-ftp/Downloads/MySQL-5.7/mysql-community-client-5.7.30-1.el7.x86_64.rpm
wget http://mirrors.ustc.edu.cn/mysql-ftp/Downloads/MySQL-5.7/mysql-community-common-5.7.30-1.el7.x86_64.rpm
wget http://mirrors.ustc.edu.cn/mysql-ftp/Downloads/MySQL-5.7/mysql-community-libs-5.7.30-1.el7.x86_64.rpm

yum install -y perl.x86_64
yum install -y libaio.x86_64
yum install -y net-tools.x86_64

rpm -ivh mysql-community-common-5.7.25-1.el7.x86_64.rpm
rpm -ivh mysql-community-libs-5.7.25-1.el7.x86_64.rpm
rpm -ivh mysql-community-client-5.7.25-1.el7.x86_64.rpm
rpm -ivh mysql-community-server-5.7.25-1.el7.x86_64.rpm


service mysqld.service restart

grep 'temporary password' /var/log/mysqld.log
```
## 国内腾讯源：
```
vim /etc/yum.repos.d/mysql-community.repo

[mysql57-community]
name=MySQL 5.7 Community Server
baseurl=https://mirrors.cloud.tencent.com/mysql/yum/mysql-5.7-community-el7-x86_64/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql

yum install mysql-community-server
```