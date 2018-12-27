# Linux Environment Configuration

## 添加 JAVA 环境，修改 profile

$sudo gedit /etc/profile

export JAVA_HOME=/usr/local/jdk1.8.0_144
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH

$source /etc/profile



## SSH 安装设置

查看当前IP： ifconfig

首先更新源：sudo apt-get update

查看是否安装SSH： ssh localhost

安装： sudo apt-get install openssh-server

启动之前检查： ps -e | grep ssh (出现sshd则安装成功)

启动： SSH:  service ssh start

SSH配置:   sido  gedit /etc/ssh/sshd_config 

数据传输：http://www.cnblogs.com/asyang1/p/9467646.html

1、配置ssh-server，配置文件位于/etc/ssh/sshd_config，默认端口为22，为了安全，一般自定义为其他端口）

2、PermitRootLogin prohibit-password，加上#注释，在后边加上一句：PermitRootLogin  yes,然后保存

重启：sudo /etc/init.d/ssh resart

## 解决 E: Unable to lock the administration directory (/var/lib/dpkg/), is another process using it?

输入：

sudo rm /var/cache/apt/archives/lock

sudo rm /var/lib/dpkg/lock

无效则输入：

sudo rm /var/lib/dpkg/lock

sudo rm /var/lib/dpkg/lock

sudo dpkg --configure -a

## 在线安装 JDK JRE OpenJDK Oracle JDK

https://linux.cn/article-3792-1.html

## Permission denied, please try again. 解决办法

修改/etc/ssh/sshd_config文件中PermitRootLogin。

PermitRootLogin without-password >> PermitRootLogin Yes   

## Ubuntu 提示sudo: java: command not found解决办法     
https://www.cnblogs.com/luminousjj/p/8308759.html

