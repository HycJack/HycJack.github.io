---
layout: post
title: Linux系统jenkins忘记管理员密码
tags: CI
---

最近购买了阿里云的服务器，实践一下利用Jenkins从git拉取代码自动部署的集成方案，由于之前安装过Jenkins，但是忘记了密码，所以记录这篇文章。

安装完Jenkins，进行初始配置后，忘记了管理员密码，找回方式：

一、 Jenkins初始密码的位置 ：

如果为Linux centos6系统，则初始密码的位置在 根目录的隐藏文件夹下面：root/.jenkins/secrets/ 下面，initialAdminPassword文件里面，编辑即可以找到；

初始密码用过之后，设置了新管理员密码后，便不再有效；

二 、 找回Jenkins的管理员密码：

网上有很多方式，改密码等；但最后选择了，改配置文件+改密码+恢复配置文件的方式；

步骤：

1. 复制 root/.jenkins/ 目录下面的config.xml文件，备份为config.xml.bak文件；

2. 修改config.xml 文件；删除下图红框部分内容，即<useSecurity>、<authorizationStrategy>、<securityRealm>节点，并保存；

3. 重启搭载Jenkins服务的tomcat；

4. 访问Jenkins地址，发现Jenkins不再需要登录；

5. 进入首页>“系统管理”>“Configure Global Security”，勾选“启用安全”；

6. 在”访问控制>安全域”里面  ，勾选 “jenkins专有用户数据>允许用户注册”；

7. 重启搭载Jenkins服务的tomcat后，访问Jenkins目录后，发现“系统管理”里有“管理用户”了；

8. 重新创建用户后，将 ~/root/.jenkins/ 目录下面备份的config.xml删除，将config.xml.bak文件复制为config.xml；

9. 重启tomcat，重新访问Jenkins，用新建的账号登录即可；