---
title: Android is GFWed
---

...前几天开始我的 Magic 就不能同步联系人，更新 Gmail 了...一开始还没有想到，以为是网络的问题，上网一看果然是 Google 相关的服务被GFWed了...顿时大感快感，又可以运动了，当然是翻墙运动。好在这次仅仅通过修改 hosts 即可解决，也就是说这次是 DNS 污染，DNS 污染就是指当我们输入一个域名，如 [http://www.google.com](http://www.google.com)的时候，解析这个域名的中国某服务商并没有返回一个正确的 IP 地址，从而导致无法登陆。话不多说，让我们修改Android里面的hosts文件。新建一个 hosts 的文件，输入...

    127.0.0.1 localhost
    74.125.93.113 android.clients.google.com

其中第二行就是说其实真正将 Android 相关服务的域名转向真正的 IP 地址。然后就简单了，连接USB，打开CMD，输入...

    adb push hosts /system/etc/hosts

然后尽情Android吧。