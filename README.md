
# Linux Environment Configuration

* [Java](#添加JAVA环境，修改profile。)
* [SHH](#ssh-安装设置)
* [Hadoop](#Hadoop配置)

## 添加JAVA环境，修改profile。
```
$sudo gedit /etc/profile
$sudo vim /etc/profile  
```
```
export JAVA_HOME=/usr/local/jdk1.8.0_144  #在这里设置jdk解压文件路径
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```
```
$source /etc/profile
```

## ZooKeeper设置    

https://blog.csdn.net/u014394255/article/details/53980656   



## SSH 安装设置

查看当前IP： ```ifconfig```

首先更新源：```sudo apt-get update```

查看是否安装SSH： ```ssh localhost```

安装： ```sudo apt-get install openssh-server```

启动之前检查：``` ps -e | grep ssh``` (出现sshd则安装成功)

启动：``` SSH:  service ssh start```

SSH配置: ```  sudo  gedit /etc/ssh/sshd_config```



数据传输：http://www.cnblogs.com/asyang1/p/9467646.html

1、配置ssh-server，配置文件位于/etc/ssh/sshd_config，默认端口为22，为了安全，一般自定义为其他端口）

2、PermitRootLogin prohibit-password，加上#注释，在后边加上一句：PermitRootLogin  yes,然后保存

重启：`sudo /etc/init.d/ssh resart`

免密匙登陆：    
https://www.cnblogs.com/ivan0626/p/4144277.html   
`ssh-keygen -t rsa`
`cat id_rsa.pub >> authorized_keys`

SSH免密匙登陆注意事项：SSH文件夹权限700  authorized_keys文件权限600（chmod）  所属用户均为root用户(chown指令 sudo chown root:root /root/.ssh/你的文件)

免密匙登陆：    
https://www.cnblogs.com/ivan0626/p/4144277.html   
`ssh-keygen -t rsa`
cat id_rsa.pub >> authorized_keys
SSH免密匙登陆注意事项：SSH文件夹权限700  authorized_keys文件权限600（chmod）  所属用户均为root用户(chown指令 sudo chown root:root /root/.ssh/你的文件)

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



## Alluxio Zookeeper 配置

alluxio.master.hostname=10.10.10.131    
alluxio.underfs.address=hdfs://10.10.10.10.131:9000/alluxio/root/    
alluxio.master.journal.forlder=hdfs://10.10.10.131:9000/alluxio/journal/     

alluxio.zookeeper.enabled=true     
alluxio.zookeeper.address=[10.10.10.131]:2181,[10.10.10.135]:2181,[10.10.10.136]:2181      


tickTime=2000    
dataDir=/home/alluxio1031/zookeeper/data    
dataLogDir=/home/alluxio1031/zookeeper/logs   
clientPort=2181   
initLimit=5   
syncLimit=2     
server.1=10.10.10.136:2181      
server.2=10.10.10.131:2181      
server.3=10.10.10.135:2181      

##  ubuntu提升管理员权限的办法         



sudo命令用来以其他身份来执行命令，预设的身份为root。在/etc/sudoers中设置了可执行sudo指令的用户。若其未经授权的用户企图使用sudo，则会发出警告的邮件给管理员。用户使用sudo时，必须先输入密码，之后有5分钟的有效期限，超过期限则必须重新输入密码。

###  语法   
sudo(选项)(参数)    
例如：sudo passwd root   #修改root的密码    
###  赋予普通用户root权限：
修改 /etc/sudoers 文件，找到下面一行，##Allows people in group wheel to run all commands    
        root ALL=(ALL) ALL    
        然后添加一行，获取root权限   
　      　qie  ALL=(ALL)  ALL   （qie是我的用户名）     
        修改完毕，现在可以用qie帐号登录，然后用命令 sudo(选项)(参数) ，即可获得临时root权限进行操作。   
 ps:这里说下你可以sudoers添加下面四行中任意一条     
    qie            ALL=(ALL)                ALL    
    %qie           ALL=(ALL)                ALL       
    qie            ALL=(ALL)                NOPASSWD: ALL      
    %qie           ALL=(ALL)                NOPASSWD: ALL      
第一行:允许用户qie执行sudo命令(需要输入密码).      
第二行:允许用户组qie里面的用户执行sudo命令(需要输入密码).      
第三行:允许用户qie执行sudo命令,并且在执行的时候不输入密码.      
第四行:允许用户组qie里面的用户执行sudo命令,并且在执行的时候不输入密码.      
https://blog.csdn.net/q290994/article/details/77448626


## Alluxio Zookeeper 配置

alluxio.master.hostname=10.10.10.131    
alluxio.underfs.address=hdfs://10.10.10.10.131:9000/alluxio/root/    
alluxio.master.journal.forlder=hdfs://10.10.10.131:9000/alluxio/journal/     

alluxio.zookeeper.enabled=true     
alluxio.zookeeper.address=[10.10.10.131]:2181,[10.10.10.135]:2181,[10.10.10.136]:2181      


tickTime=2000    
dataDir=/home/alluxio1031/zookeeper/data    
dataLogDir=/home/alluxio1031/zookeeper/logs   
clientPort=2181   
initLimit=5   
syncLimit=2     
server.1=10.10.10.136:2181      
server.2=10.10.10.131:2181      
server.3=10.10.10.135:2181      

##  ubuntu提升管理员权限的办法    



sudo命令用来以其他身份来执行命令，预设的身份为root。在/etc/sudoers中设置了可执行sudo指令的用户。若其未经授权的用户企图使用sudo，则会发出警告的邮件给管理员。用户使用sudo时，必须先输入密码，之后有5分钟的有效期限，超过期限则必须重新输入密码。

###  语法   
sudo(选项)(参数)    
例如：sudo passwd root   #修改root密码    
###  赋予普通用户root权限：
修改 /etc/sudoers 文件，找到下面一行，##Allows people in group wheel to run all commands    
        root ALL=(ALL) ALL    
        然后添加一行，获取root权限   
　　qie  ALL=(ALL)  ALL   （qie是我的用户名）     
        修改完毕，现在可以用qie帐号登录，然后用命令 sudo(选项)(参数) ，即可获得临时root权限进行操作。   
 ps:这里说下你可以sudoers添加下面四行中任意一条     
    qie            ALL=(ALL)                ALL    
    %qie           ALL=(ALL)                ALL       
    qie            ALL=(ALL)                NOPASSWD: ALL      
    %qie           ALL=(ALL)                NOPASSWD: ALL      
第一行:允许用户qie执行sudo命令(需要输入密码).      
第二行:允许用户组qie里面的用户执行sudo命令(需要输入密码).      
第三行:允许用户qie执行sudo命令,并且在执行的时候不输入密码.      
第四行:允许用户组qie里面的用户执行sudo命令,并且在执行的时候不输入密码.      
https://blog.csdn.net/q290994/article/details/77448626

## Hadoop配置

https://blog.csdn.net/sinat_25943197/article/details/81700842   
https://blog.csdn.net/dream_an/article/details/80258283   
https://blog.csdn.net/u010366748/article/details/82843454#comments    
