---
layout: post
title: vncserver 配置
---

# **vncserver**配置


标签（空格分隔）： vnc

---
linux下vncserver的配置文件都位于`~/.vnc/xstartup`.但是，系统默认的桌面环境不同，配置文件不同。
在ONOS开发中，目前使用的虚拟机镜像的默认桌面环境是LXDE，按照第二种方式来配置即可。

##桌面环境为GNOME的vncserver配置
将xstartup修改为如下配置并保存。
```shell
linux-4gwx:~ # cat ~/.vnc/xstartup 
#!/bin/sh

xrdb $HOME/.Xresources
xsetroot -solid grey
xterm -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
#twm &
gnome-session &
```
保存完毕后重启vncserver即可。
##桌面环境为LXDE的vncserver配置
将xstartup修改为如下配置并保存。
```shell
linux-4gwx:~ # cat ~/.vnc/xstartup 
# Uncomment the following two lines for normal desktop:
# unset SESSION_MANAGER
# exec /etc/X11/xinit/xinitrc

[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &
x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
#x-window-manager &
lxterminal & /usr/bin/lxsession -s LXDE &
```
##重启vncserver
如果已经启动了vncserver，需要先关闭对应的启动端口，然后再启动，设置才会生效。
 1. 关闭vncserver `vncserver -kill :1`
 2. 启动vncserver `vncserver -geometry 1640x960 :1`
> **NOTE:** 关闭命令中，`-kill` 和 `:1`之前有个空格；启动命令中`1640x960`是登录后的屏幕分辨率，需要根据具体情况设定。
