---
title: Android Skill
date: 2020-03-07 13:42:47

categories:
- [Android, Skill]

tags:
---

## 打开Url Scheme协议链接

```shell
adb shell am start -a android.intent.action.VIEW -d "snssdk1128://user/profile/3733569708763603"
```



## 将用户证书修改为系统证书

```shell
adb shell
su
mount -o remount,rw /system
ls -al /data/misc/user/0/cacerts-added/
cp /data/misc/user/0/cacerts-added/* /etc/security/cacerts/*
rm /data/misc/user/0/cacerts-added/*
chmod 644 /etc/security/cacerts/*
chown root:root /etc/security/cacerts/*
```

