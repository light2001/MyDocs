# 文档类项目
文档类项目，自己的所有文档整理


### 根据日常需要，主要包括以下几类日志：
1. 运维类
2. 研发类
3. 技术类
4. 设计类
5. 项目类


#### 运维文档
1. Centos教程
        1. [在Centos环境下安装Docker ce](/运维文档/Centos安装Docker.md)
        2. [Centos环境下防火墙入口配置](/运维文档/Centos环境下防火墙入口配置.md)
        3. [Cenots环境下如何安装Docker下的禅道](https://blog.csdn.net/qq_28039297/article/details/78650552)
        4. [Centos环境下如何安装Docker下的gitlab](https://www.cnblogs.com/xuezhigu/p/6555895.html)
        5. [Centos下安装Docker下的Mysql，并启动](https://www.linuxidc.com/Linux/2017-09/146659.htm)
        6. [Centos下安装Nodejs最新版的三种方式](https://blog.csdn.net/bbwangj/article/details/82253785)
        7. [在centos7安装nginx](https://blog.csdn.net/oldguncm/article/details/78855000)
        8. [Centos7 安装Chrome浏览器](https://www.cnblogs.com/ianduin/p/8727333.html)
2. Ubuntu教程
        1. [Ubuntu怎么安装最新的nodejs](https://blog.csdn.net/chenyao1994/article/details/82495163)
        2. [Ubuntu怎么安装Chrome](https://www.cnblogs.com/cainiaoaixuexi/p/9033350.html)
        3. [Ubuntu 分辨率高以后，解决缩放问题](http://tieba.baidu.com/p/5670339451)
        4. [Ubuntu 怎么安装Nodejs最新版](/运维文档/Ubuntu安装Nodejs.md)
        5. [Ubuntu 怎么安装最新版的git](/运维文档/Ubuntu安装Git最新版.md)
        6. [ubuntu 18 更换软件源](https://blog.csdn.net/zhangjiahao14/article/details/80554616)
        7. [ubuntu 18 安装搜狗输入法](https://blog.csdn.net/lupengCSDN/article/details/80279177)
3. Docker
        1. [Docker如何配置加速器](https://blog.csdn.net/bwlab/article/details/50542261)
        2. [阿里云Docker加速服务，如何使用](https://www.cnblogs.com/zhxshseu/p/5970a5a763c8fe2b01cd2eb63a8622b2.html)
        3. [Docker下，连接到已经打开的容器](https://www.cnblogs.com/zhuxiaojie/p/5947270.html)
        4. [删除Docker镜像](https://www.cnblogs.com/q4486233/p/6482711.html)
        5. [如果国内无法安装docker-ce，可以使用阿里的镜像仓库](https://blog.csdn.net/yohoph/article/details/80079078)
4. Nginx
        1. [nginx端口转发因为selinx无法运行，不关闭selinux的解决办法](https://blog.csdn.net/babys/article/details/54135438)
5. Windows
        1. [WindowsServer2016安装DockerForWindows](https://baijiahao.baidu.com/s?id=1570288005533351&wfr=spider&for=pc)
        2. [在Windows下部署将Solr7.2.1部署在Tomcat9下](/运维文档/Solr7部署.md)
6. 通用Linux
        1. [在Linux下生成SSH Key，然后免key登陆GitLab](https://blog.csdn.net/y1574406771/article/details/72676980)
7. Git相关
        1. [工作中常见git问题汇总](/编程文档/git/main.md)



### 实战演练
1. [在centos7.5环境下配置实现.net core项目的自动化部署](/实战演练/自动化部署/main.md)

### 开发语言
1. [go语言环境配置](https://blog.csdn.net/u013295518/article/details/78766086)

#### 已安装的Docker镜像,全部来自官方镜像仓库
1. nginx
2. tomcat
3. solr
4. elasticsearch
5. redis
6. postgres
7. mysql
8. mongo
9. gitlab
10. zentao

###### 在docker pull后运行禅道
```
mkdir -p /data/zbox && docker run -d -p 81:80 -p 3306:3306 \
        -e USER="root" -e PASSWD="password" \
        -e BIND_ADDRESS="false" \
        -e SMTP_HOST="163.177.90.125 smtp.exmail.qq.com" \
        -v /data/zbox/:/opt/zbox/ \
        --privileged=true \
        --name zentao-server \
        idoop/zentao:latest

```

#### 教程
1. [Docker在线教程](https://yeasy.gitbooks.io/docker_practice/content/)
2. [阮一峰的Docker入门教程](http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)


#### 完整版教材
1. [Docker入门到实践，这个强推](https://www.gitbook.com/book/yeasy/docker_practice/details)


#### 专项课题
1. [win10环境安装Hyper-v虚拟机](/运维文档/在win10操作系统下安装Hyper-v.md)
2. [基于Hyper-v安装Centos7.5](/运维文档/通过Hyper-v安装Centos7.5.md)
3. [Centos7.5常用软件以及Docker的安装](/运维文档/在纯净的Centos7.5下安装常用软件和Docker.md)
4. [Docker常用操作以及容器安装运行](/运维文档/基于Docker安装和运行常用容器.md)
