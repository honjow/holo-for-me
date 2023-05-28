# GPD WinMax2 蓝牙连接Xbox手柄异常的问题

## 问题描述

在使用Xbox手柄蓝牙方式连接时，手柄会在连接成功后不久冻结，无法使用。但是连接不会断开。

## 解决方案

禁用蓝牙自动休眠功能

添加udev规则

```bash
sudo vim /etc/udev/rules.d/99-disable-bluetooth-autosuspend.rules

# 添加以下内容
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="8087", ATTRS{idProduct}=="0032", ATTR{power/autosuspend}="-1"
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="8087", ATTRS{idProduct}=="0032", TEST=="power/control", ATTR{power/control}="on"
```
