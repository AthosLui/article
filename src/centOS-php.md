# centOS 安装 php 环境

## yum

`yum list installed`：查看已经安装的包  
`yum -y install packageName`：安装包「-y 表示所有的对话都选择同意」
`yum -y remove packageName`：卸载包「-y 表示所有的对话都选择同意」


## 安装 Apache

1. `yum install httpd` 安装 Apache
1. 浏览器输入 IP 地址就可以访问了

## 安装 php

1. `yum install php` 安装 php
1. `service httpd restart` 重启 Apache
1. 浏览器输入 IP 地址就能看到 phpInfo 了
