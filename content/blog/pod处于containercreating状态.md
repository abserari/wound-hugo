+++
author = "Abser"
categories = ["k8s"]
date = 2018-12-08T13:45:31+08:00
description = "k8s,yaml创建pod不成功"
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Pod处于containercreating状态"
type = "post"

+++

## 问题

用k8s创建完pod后，查了一下pods状态，发现都在containercreationg状态中

 ==> kubectl get pods

## 原因分析

用kubectl describe查看 pods的详情,发现 registry.access.redhat.com/rhel7/pod-infrastructure:latest 镜像报错

 `==> kubectl describe pod mysql`



使用docker pull  拉取镜像，提示缺失rhsm 文件

`==> docker pull registry.access.redhat.com/rhel7/pod-infrastructure:latest`

##解决方案

yum 安装 rhsm，发现 python-rhsm-certificates  已被 subscription-manager-rhsm-certificates 替换，无法yum 成功

`==> yum install *rhsm*`



使用 wget 获取python-rhsm-certificates-1.19.10-1.el7_4.x86_64.rpm  rpm包并安装 python-rhsm-certificates

`==>wget http://mirror.centos.org/centos/7/os/x86_64/Packages/python-rhsm-certificates-1.19.10-1.el7_4.x86_64.rpm`

`==>rpm2cpio python-rhsm-certificates-1.19.10-1.el7_4.x86_64.rpm | cpio -iv --to-stdout ./etc/rhsm/ca/redhat-uep.pem | tee /etc/rhsm/ca/redhat-uep.pem`

 

再次使用使用docker pull  拉取镜像

`==> docker pull registry.access.redhat.com/rhel7/pod-infrastructure:latest`

## 成功

pods 已成功 在Running 状态中

 `==> kubectl get pods`

---------------------
