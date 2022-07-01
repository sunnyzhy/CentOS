# 安装centos7

## 1. 安装

1. Install CentOS 7

2. 选择系统的语言 -> Continue

3. INSTALLATION SUMMARY

SOFTWARE -> SOFTWARE SELECTION -> GNOME Desktop

SYSTEM -> INSTALLATION DESTINATION -> Device Selection -> Select Local Standard Disks

4. Begin Insatllation

5. USER SETTINGS
ROOT PASSWORD
USER CREATION

6. Finish configuration

7. Reboot

8. Initial setup of CentOS Linux 7 (Core)

输入"1"，按Enter键；输入"2"，按Enter键；输入"q"，按Enter键；输入"yes"，按Enter键

9. 登录CentOS

10. 选择汉语 -> 前进；选择输入法 -> 前进

11. 设置系统时间

All Settings -> System -> Date & Time -> Time Zone -> CST (Shanghai, China)

## 2. 添加桌面快捷方式

```/usr/share/applications``` -> 右击对应的图标Copy，然后Paste到桌面

## 3. 取消屏幕保护自动锁屏功能

```All Settings -> Privacy -> Screen Lock -> Automatic Screen Lock (OFF) & Show Notifications (OFF)```

## 4. 添加中文输入法

```All Settings -> Region & Language -> Input Sources -> + -> Chinese (Intelligent Pinyin)```

## 5. 修改 yum 源

```bash
# cd /etc/yum.repos.d

# cp CentOS-Base.repo CentOS-Base.repo.backup

# wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

# yum install -y epel-release
```
