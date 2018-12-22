# Linux Environment Configuration

## 添加JAVA环境，修改profile

$sudo gedit /etc/profile

export JAVA_HOME=/usr/local/jdk1.8.0_144
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH

$source /etc/profile



## SSH安装设置
查看当前IP： ifconfig
查看是否安装SSH： ssh localhost
安装： sudo apt-get install openssh-server
启动之前检查： ps -e | grep ssh (出现sshd则安装成功)
启动： SSH:  service ssh start

SSH配置:   sido  gedit /etc/ssh/sshd_config

PermitRootLogin prohibit-password，加上#注释

在后边加上一句：PermitRootLogin  yes,然后保存

