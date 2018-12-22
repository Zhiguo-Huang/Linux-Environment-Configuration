# Linux Environment Configuration

# 添加JAVA环境，修改profile

$sudo gedit /etc/profile

export JAVA_HOME=/usr/local/jdk1.8.0_144
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH

$source /etc/profile
