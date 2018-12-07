+++
author = "Abser"
categories = ["ssh"]
date = 2018-12-07T12:27:27+08:00
description = "Permission denied (publickey,gssapi-keyex,gssapi-with-mic)"
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Ssh连接"
type = "post"

+++

## 问题

ssh远程连接服务器

提示：`Permission denied (publickey,gssapi-keyex,gssapi-with-mic)`

## 原因分析

参数 `PasswordAuthentication` 的默认值为 `yes`，SSH服务将其值置为 `no` 以禁用密码验证登录，导致此类故障。需要修改 `PasswordAuthentication` 配置解决此问题。

## 解决方法

###在服务端执行

* 执行命令 `vi /etc/ssh/sshd_config`，按下 `i` 编辑SSH服务配置文件，将参数 `PasswordAuthentication` 设置为 `yes`，或者在 `PasswordAuthentication` 参数前添加井号（#），按下 `Esc` 退出编辑模式，并输入 `:wq` 保存退出。

  [![Shooting](https://gw.alipayobjects.com/zos/onekb/MTPVMOAoDmUUXvTkPGQv.png)](https://gw.alipayobjects.com/zos/onekb/MTPVMOAoDmUUXvTkPGQv.png)

* 执行命令 `service ssh restart` 重启SSH服务。

  > **说明**：如果您使用CentOS 7及以上，执行命令 `systemctl restart sshd` 重启SSH服务。

### 在使用端执行

* 记得删除之前连接时添加的known_host记录

> **说明**：通常在  `<用户名>/.ssh/`  目录下

