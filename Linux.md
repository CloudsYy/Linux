## Linux常用命令总结

### 一、(ubuntu)Linux初始化配置：

    1.sudo apt-get install ssh -y (1，2一般都已经完成安装了。)

    2.sudo apt-get install vim -y
    
    3.sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
    备注：备份源文件（这里相当于pom文件，根据源，下载对应的包)

    4.sudo vi /etc/apt/sources.list 

### 二、以下为阿里云的源：
    deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
    
    deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
    
    deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
    
    deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
    
    deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
    deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
## 对数据源的操作
### 1.修改了源文件后，更新源
    sudo apt-get update
### 2.升级所有源软件包
    sudo apt-get upgrade -y
## 三、重启systemd-logind服务
    systemctl restart systemd-logind

## 安装ifconfig,可以查看网络状态
    sudo apt-get install net-tools -y 
## 对docker的操作    
#### 1、安装docker镜像
    sudo apt install docker.io -y
#### 2、查看docker版本    
    sudo docker --version
#### 3、查看docker详细的信息   
    sudo docker info

#### 4、sudo vi /etc/docker/daemon.json (查看并修改docker加载源)    
    {
        "registry-mirrors": ["http://hub-mirror.c.163.com"]
    }

#### 5、重启docker容器
    sudo service docker restart
#### 6、开启docker容器
    systemctl start docker
#### 7、查看docker容器状态
    systemctl status docker
## 移动文件
    mv jdk-8u152-linux-x64.tar.gz /usr/local/lib
## 切换java环境，如果有多个jdk的话
    sudo update-alternatives --config java
## 配置java环境环境
    sudo vi ~/.bashrc (以下为配置java环境)：
    方式一：
    1.export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_191(这里要注意目录要换成自己解压的jdk目录)

    2.export JRE_HOME=${JAVA_HOME}/jre 

    3.export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib 

    4.export PATH=${JAVA_HOME}/bin:$PATH
    
    5.source ~/.bashrc
    
    6.sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_191/bin/java 300
    
    7.java -version(查看java版本)
    
    方式二：
    1.set JAVA_HOME=/usr/lib/jvm/java-6-sun-1.6.0.15
    
    2.export JAVA_HOME
    
    3.set PATH=$JAVA_HOME/bin:$PATH
    
    4.export PATH
    
    5.set CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
    
    6.export CLASSPATH
    
    格式：set (需要加的变量名)name=路径	
    
    export 变量名name
## docker安装部署minio：
    1.docker pull minio/minio (安装minio)
    
    2.docker run -p 9000:9000 --name minio-iot -v /mnt/data:/data -v /mnt/config:/root/.minio minio/minio server /data
    
    3.查找这个目录是哪个应用mount 过来： mount -l |more
    
    4.查找文件：find -name *.xlsx
    
    5.-- 备注： 运行安装已经下在的minio : 9000：9000 第一个是外部接口，第二个是内部接口， server 安装到 data
    
    6.docker run -p 9000:9000 minio/minio server /data
    
    7.-- tmus 可以共享命令
    
    8.查看端口：ps -aux |grep  docker
    
    9.检查docker安装：netstat -an |more docker
    
    10.dpkg --list|grep mysql
    
    11.sudo apt-get remove mysql-common（这个为例子，可以根据list中删除）
    
    12.dpkg -l|grep ^rc|awk '{print$2}'|sudo xargs dpkg -P(清除残留痕迹数据(mysql))
    
    13.linux 中的保存，:wq保存且退出、 q!不保存强行退出、x保存退出、
    
    14.ls / ls -a / ls -al
    
    15.docker exec -it ****  /bin/bash or sh	进入docker

## 文件
    drwxr-xr-x 2 root root 4096 Jan 16 17:24 9a7fe28b-2da4-4887-9d6b-39d6f75170b9
    -rw-r--r-- 1 root root  147 Jan 16 17:24 data-usage
    d 为文件
    - 为文件夹
## 查看服务器磁盘信息
    df -h 
## 查看服务器cpu信息
    top 
## 图标(可运行文件，类似于windows的exe文件等)
    ls ll 其中黄色为硬链接，白色为软链接，软链接相当于图标，修改这个图标不会修改文件本身的内容
