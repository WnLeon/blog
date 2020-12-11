---
layout: post
title: "MySQL删除root用户后恢复 "
categories: home
tags: " "
excerpt_separator: <!--more-->
--- 

 MySQL删除root用户后恢复
<!--more-->

##  MySQL数据库中有一个超级特权用户，那就是root。root用户有至高无上的权限，它可以创建数据库，创建用户，赋予用户权限，对所以数据库拥有所有的操作权限。一旦这个用户被删除了会怎么样呢，我们可想而知。总之，MySQL中不能没有它，那么如果root用户被删除后，该怎么恢复呢？且看下文。

首先，跟忘记root用户密码差不多，需要设置MySQL跳过权限检查。

1、用系统管理员登陆系统。

2、停止MySQL的服务，命令：net stop mysql

3、进入命令窗口，然后进入MySQL的安装目录，比如我的安装目录是c:\mysql,进入C:\mysql\bin

4、跳过权限检查启动MySQL，执行 c:\mysqlbin>mysqld-nt --skip-grant-tables。这个窗口暂时就留给它用了，等会儿用完后再关闭。如果现在就关闭，那MySQL也会跟着被关闭。

这样就启动了一个不需要密码的MySQL实例进程。接下来就登陆进去，重新创建MySQL用户。

5、C:\mysql\bin>mysql -uroot -p，提示输入密码的时候随便输入什么都可以进去。或者，直接C:\mysql\bin>mysql就可以进去了。

6、然后，use mysql，往mysql的user表中插入一条root用户的记录。
```
insert into user set user='root',ssl_cipher='',x509_issuer='',x509_subject='',authentication_string=password('123.com');
update user set Host='localhost',select_priv='y', insert_priv='y',update_priv='y',Alter_priv='y',delete_priv='y',create_priv='y',drop_priv='y',reload_priv='y',shutdown_priv='y',Process_priv='y',file_priv='y',grant_priv='y',References_priv='y',index_priv='y',show_db_priv='y',super_priv='y',create_tmp_table_priv='y',Lock_tables_priv='y',execute_priv='y',repl_slave_priv='y',repl_client_priv='y',create_view_priv='y',show_view_priv='y',create_routine_priv='y',alter_routine_priv='y',create_user_priv='y' where user='root';
```

7、然后退出MySQL，再以有权限检查的方式登陆进来。（先关闭运行mysqld-nt --skip-grant-tables时的窗口，再运行net start mysql）

8、运行C:\mysql\bin>mysql -uroot -p，这个时候密码本身为空，直接回车就可登陆进去。

9、修改root密码，mysql> update user set password=password('123456') where user='root';

这样就大功告成了，再善后一下

10、mysql> flush privileges; mysql> exit;