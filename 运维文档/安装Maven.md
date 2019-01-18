### Maven介绍

  Maven是apache的软件包管理项目，用于Java项目的
  包，组件管理，类似.Net的Nuget，有人说比Nuget还要强大，暂时没有感受，不过使用起来入门还是很简单的

  安装maven需要先安装jdk，本文会默认你已经安装上jdk了


#### 安装步骤
- 打开maven官网，找到下载地址，然后复制到ssh终端里用wget下载
```
wget http://mirror.bit.edu.cn/apache/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz

```

- 解压缩刚才下载的文件,并修改文件夹名称

```
tar -zxvf apache-maven-3.6.0-bin.tar.gz
mv apache-maven-3.6.0-bin.tar.gz maven

```

- 用vim打开/etc/profile，这个文件，在最后面增加以下几行代码(maven的目录设置为/home/maven)

```
export M2_HOME=/home/maven
export PATH=$PATH:$M2_HOME/bin

```

- 用mvn -v 命令查看是否安装成功,如果看到如下命令，则表示已经安装成功了

```
[root@localhost ~]# mvn -v

Apache Maven 3.6.0(1edded0938998edf8bf061f1ceb3cfdeccf443fe; 2018-06-18T02:33:14+08:00)
Maven home: /home/maven
Java version: 1.8.0_201, vendor: Oracle Corporation, runtime: /usr/java/jdk1.8.0_201-amd64/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "3.10.0-957.1.3.el7.x86_64", arch: "amd64", family: "unix"
```


- 配置maven的本地仓库地址，打开/home/maven/conf目录，找到settings.xml，找到下面这部分，修改成你要的目录

```
 # 以下注释部分可以手动调整结束符
  <!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  -->
  <localRepository>/home/maven/repo</localRepository>

```