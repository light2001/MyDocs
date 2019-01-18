### JAVA介绍

  JAVA是目前全球占比最大的开发语言，这个就不多做介绍了

#### RPM 安装操作 

  命令： 
  rpm -i 需要安装的包文件名 
  举例如下： 
  rpm -i example.rpm 安装 example.rpm 包； 
  rpm -iv example.rpm 安装 example.rpm 包并在安装过程中显示正在安装的文件信息； 
  rpm -ivh example.rpm 安装 example.rpm 包并在安装过程中显示正在安装的文件信息及安装进度； 
  RPM 查询操作 



#### 安装步骤
- 打开Oracle官网，找到JDK下载地址，然后复制到ssh终端里用wget下载,或者从windows上下载，传送到centos服务器下
```
wget https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-i586.rpm

```

- 通过RPM命令安装rpm包

```
rpm -ivh jdk-8u201-linux-i586.rpm

```

- 用java -version 命令查看是否安装成功,如果看到如下命令，则表示已经安装成功了

```
[root@localhost conf]# java -version
java version "1.8.0_201"
Java(TM) SE Runtime Environment (build 1.8.0_201-b09)
Java HotSpot(TM) 64-Bit Server VM (build 25.201-b09, mixed mode)
[root@localhost conf]# 

```
