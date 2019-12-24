---
layout: post
title: 如何在 WSL Ubuntu 中安装根证书？
date: 2019-12-24 16:04 +0800
---
给定 CA 证书文件 `foo.crt`，按照以下步骤在 WSL Ubuntu 中安装根证书：

1. 在系统存放证书的位置 `/usr/share/ca-certificates` 创建一个新的目录：

   ```shell
   sudo mkdir /usr/share/ca-certificates/custom
   ```

2. 复制 `foo.crt` 到新创建的目录：

   ```shell
   sudo cp foo.crt /usr/share/ca-certificates/custom/foo.crt
   ```

3. 要让新证书生效，还需要更新系统证书配置：

   ```shell
   sudo dpkg-reconfigure ca-certificates
   ```

   执行这条交互式命令，将新证书加到系统证书配置。这样，新证书的相对路径 `custom/foo.crt`（相对于 `/usr/share/ca-certificates`）会被追加到 `/etc/ca-certificates.conf` 中，即生效。
