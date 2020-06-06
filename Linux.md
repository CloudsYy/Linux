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
#### 8、查看本地镜像
    docker images
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
## 查看对应的版本信息，例如：mysql
    docker search mysql
## 查看日志
    docker logs -f mysql
## 进入mysql
    1.docker exec -it mysql bash
    2.mysql -uroot -p
    接着输入密码，进入mysql内部
    3.show databases;
    接下来，可进行数据库操作.
## 查看tcp进程(端口占用情况)
    netstat -tanlp
## 杀死进程(根据PID)
    sudo kill 18042
### 关于数据库操作的命令(Linux)-----→[linux 查看数据库和表 mysql 命令](https://my.oschina.net/u/3482619/blog/1613914)
#### 连接远程服务器
    1.use mysql;
    2.select host,user,plugin,authentication_string from mysql.user;
    3.ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '****';
    4.ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '****';

### rar文件解压命令
    1.压缩rar文件：rar a -r test.rar file
    2.解压文件：unrar x test.rar
    释义：
    a : 添加到压缩文件
    -r : 递归处理
    x : 以绝对路径解压文件
    
### tar文件解压命令
    1.压缩文件 file1 和目录 dir2 到 test.tar.gz
    tar -zcvf test.tar.gz file1 dir2
    2.解压 test.tar.gz（将 c 换成 x 即可）
    tar -zxvf test.tar.gz
    3.列出压缩文件的内容
    tar -ztvf test.tar.gz 
    释义：
    -z : 使用 gzip 来压缩和解压文件
    -v : --verbose 详细的列出处理的文件
    -f : --file=ARCHIVE 使用档案文件或设备，这个选项通常是必选的
    -c : --create 创建一个新的归档（压缩包）
    -x : 从压缩包中解出文件
    
### 解压zip文件：
    1.压缩文件
    zip -r test.zip file
    2.解压文件
    zip test.zip
    释义：
    -r : 递归处理
    
### docker文件复制
    1.从宿主机复制文件到docker容器
    docker cp <host_path/file_name> <contaioner_name>:<path>
    2.从docker容器复制文件到宿主机
    docker cp <contaioner_name>:<path/file_name> <host_path>   
    
### du的用法
    du -sh : 查看当前目录总共占的容量。而不单独列出各子项占用的容量 
    
    du -lh --max-depth=1 : 查看当前目录下一级子文件和子目录占用的磁盘容量。
    
    du -sh * | sort -n 统计当前文件夹(目录)大小，并按文件大小排序
    du -sk filename 查看指定文件大小

### linux 运行java程序命令
    实例:
    nohup java -jar mblog-latest.jar >mblog.log &
    
### Linux常用命令
传送阵>>>>>>[Linux常用命令](https://github.com/zhousc1994/linux-learn/blob/master/src/basicCommands/%E5%9F%BA%E7%A1%80%E5%91%BD%E4%BB%A4.md)
