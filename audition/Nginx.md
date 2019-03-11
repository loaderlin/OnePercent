四项确认

- 确认系统网络可用
- 确认yum源可用
- 确认关闭iptables规则
- 确认停用selinux

```shell
ping baidu.com

yum -y install gcc gcc-c++ autoconf pcre pcre-devel make automake
yum -y install wget httpd-tools vim

cd /opt
mkdir app download logs work backup

# 查看
iptables -L
# 关闭
iptables -F

# 查看
iptables -t nat -L
# 关闭
iptables -t nat -F

# 查看
getenforce
# 关闭
setenforce 0

```

![中间件结构](https://upload-images.jianshu.io/upload_images/10408135-e4ab4b12f73ff59a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)



## 安装Nginx

查看Linux版本（Centos版本号）

```sh
yum install redhat-lsb -y

lsb_release -a
```




