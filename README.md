# 文档类项目
该文档类项目，是自己日常工作所需的，以及自己闲暇折腾的所有技术总结，包括以下技术栈：
- .net core
- java
- spring boot
- centos
- ubuntu
- vue,vue-element-admin
- angular
- ng-alain,ng-zarro-antd
- git
- docker
- docker容器编排
- gitlab,自动化部署
- nginx

根据我工作的变化，以后还会增加

可以看出我的工作多而且杂，穿插了运维，研发（前端，后端），没办法，劳碌命


#### 代码仓库
---

#### 国内镜像地址

   如果觉得速度慢，可以访问国内的镜像地址  [https://gitee.com/light2001/MyDocs](https://gitee.com/light2001/MyDocs)

#### Github

   本项目原始地址在github上，点击可以跳转
   [https://github.com/light2001/MyDocs](https://github.com/light2001/MyDocs)

---

### 根据日常需要，主要包括以下几类文档：
- 运维类
- 研发类
- 技术类
- 设计类
- 项目类


#### 运维文档
- Centos7
   - [安装Docker ce](/运维文档/Centos安装Docker.md)
   - [防火墙配置教程](/运维文档/Centos环境下防火墙配置.md)
   - [如何安装Docker下的禅道](https://blog.csdn.net/qq_28039297/article/details/78650552)
   - [如何安装Docker下的gitlab](https://www.cnblogs.com/xuezhigu/p/6555895.html)
   - [安装Docker下的Mysql，并启动](https://www.linuxidc.com/Linux/2017-09/146659.htm)
   - [安装Nodejs最靠谱的方式](https://www.cnblogs.com/betx/p/10347797.html)
   - [安装nginx](https://blog.csdn.net/oldguncm/article/details/78855000)
   - [安装Chrome浏览器](https://www.cnblogs.com/ianduin/p/8727333.html)
   - [安装Maven](/运维文档/安装Maven.md)
   - [安装JDK8](/运维文档/安装Java.md)
   - [Hyper-v环境下，磁盘空间满，扩容处理](/运维文档/虚拟机环境下Centos7磁盘扩容.md)
   - [如何分析网络流量，使用tcpdump](./运维文档/Centos下如何使用tcpdump抓包.md)
   - [Samba连接widnows](https://blog.csdn.net/yexiangcsdn/article/details/82867469)
   - [Samba挂载windows目录](/运维文档/samba如何和windows共享交互.md)
   - [Npm部署前端项目，权限问题解决](https://www.cnblogs.com/dunke/p/10224770.html)
   - [物理机扩充硬盘](/运维文档/Centos物理机如何扩展硬盘.md)

- Ubuntu18
   - [怎么安装最新的NodeJs(采用安装方式)](https://blog.csdn.net/chenyao1994/article/details/82495163)
   - [怎么安装Chrome](https://www.cnblogs.com/cainiaoaixuexi/p/9033350.html)
   - [分辨率高以后，解决缩放问题](http://tieba.baidu.com/p/5670339451)
   - [怎么安装Nodejs最新版(采用解压缩方式)](/运维文档/Ubuntu安装Nodejs.md)
   - [怎么安装最新版的git](/运维文档/Ubuntu安装Git最新版.md)
   - [更换软件源](https://blog.csdn.net/zhangjiahao14/article/details/80554616)
   - [安装搜狗输入法](https://blog.csdn.net/lupengCSDN/article/details/80279177)
   - [安装.NetCore](https://www.cnblogs.com/xyfy/p/9881855.html)
   - [安装Deepin,Wine软件](https://www.lulinux.com/archives/1319)
- ManjaroLinux
   - [新系统折腾](https://blog.csdn.net/github_39457740/article/details/84551304)
   - [精品教程，安装后要做的事](https://www.cnblogs.com/elinuxboy/p/10123877.html)
   - [搜狗输入法](https://www.jianshu.com/p/1cde4b7ec3c2)
   - [谷歌浏览器](https://blog.51cto.com/aurogon/2321871)
   - [Docker](https://blog.csdn.net/albertjone/article/details/80266700)

- Docker
   - [连接到已经打开的容器](https://www.cnblogs.com/zhuxiaojie/p/5947270.html)
   - [删除Docker镜像](https://www.cnblogs.com/q4486233/p/6482711.html)
   - [如果国内无法安装docker-ce，可以使用阿里的镜像仓库](https://blog.csdn.net/yohoph/article/details/80079078)
   - [部署Spring Boot项目注意事项](/运维文档/SpringBoot部署.md)
   - [删除多余的虚悬镜像](/运维文档/虚悬镜像.md)
   - [Portainer.io介绍(Docker图形化管理工具)](https://www.cnblogs.com/river2005/p/8283700.html)
   - [限制Docker容器的日志容量-过大会导致磁盘空间满](/运维文档/Docker日志容量限制.md)
   - [容器导出迁移到其他机器](https://www.jianshu.com/p/4e862a2a2d03)
   - [给容器打标签-tag](https://www.cnblogs.com/weifeng1463/p/11190567.html)
   - [修改已经运行的容器参数](https://www.cnblogs.com/ExMan/p/11613148.html)
   - 镜像加速
      - [Docker阿里云加速器链接地址](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)
      - [如何配置加速器](https://blog.csdn.net/bwlab/article/details/50542261)
      - [阿里云Docker加速服务，DockerForWindows](https://www.cnblogs.com/zhxshseu/p/5970a5a763c8fe2b01cd2eb63a8622b2.html)
   - [如何安装ELK](/运维文档/安装ELK.md)
   - [Elastic-Plugin插件安装教程](https://my.oschina.net/u/2342969/blog/2252364)
   - [安装Kafka](https://www.jianshu.com/p/9552871bb40a)
   - [安装RabbitMq](https://www.cnblogs.com/angelyan/p/11218260.html)
   - [安装RocketMq](https://zhuanlan.zhihu.com/p/133792711)
   - [安装Memcached](https://blog.csdn.net/zhi_ai_yaya/article/details/90510936)

- Nginx
   - [nginx端口转发因为selinx无法运行，不关闭selinux的解决办法](https://blog.csdn.net/babys/article/details/54135438)
- Windows
   - [安装DockerForWindows](https://baijiahao.baidu.com/s?id=1570288005533351&wfr=spider&for=pc)
   - [部署将Solr7.2.1部署在Tomcat9下](/运维文档/Solr7部署.md)
- 通用Linux
   - [在Linux下生成SSH Key，然后免key登陆GitLab](https://blog.csdn.net/y1574406771/article/details/72676980)
- Git相关
   - [工作中常见git问题汇总](/编程文档/git/main.md)
   - [gitlab迁移，备份恢复](https://www.cnblogs.com/breakering/p/9712040.html)
- 自动化部署(CICD
   - Gogs
      - [Gogs安装注意事项](https://www.cnblogs.com/phpisbest/p/7000255.html)
      - [超详细教程](http://www.mdslq.cn/archives/1a623683.html)
   - Drone
      - [Drone安装调试简单教程](https://cloud.tencent.com/developer/article/1379546)
      - [Drone+gogs简化教程](https://www.jianshu.com/p/fe2521afddcf)
   - Rancher
- mysql
   - [Mysql导入导出](/运维文档/Mysql导入导出.md)
- MQTT
   - [mosquitto安装](/运维文档/Mosquitto安装使用.md)
- ELK
   - [Elasticsearch RestFul使用教程](https://blog.csdn.net/gwd1154978352/article/details/82804942)
   - [Elasticsearch增删改查演练](/运维文档/Elasticsearch测试.md)

### 开发文档
- 后端语言
   - .NetCore
      - [使用VSCode开发.NetCore](https://www.cnblogs.com/yilezhu/p/9926078.html)
      - [千星项目OpenAuth.Net基于.Net Core 2.1的快速开发框架,核心模块包括：组织机构、角色用户、权限授权、表单设计、工作流等。它的架构精良易于扩展，是中小企业的首选](https://github.com/yubaolee/OpenAuth.Core?tdsourcetag=s_pctim_aiomsg)
      - [NET, .NET CORE Open Source Workflow Engine 开源工作流引擎slickflow.com](https://github.com/besley/Slickflow?tdsourcetag=s_pctim_aiomsg)
      - [使用Identity Server 4建立Authorization Server (2)](https://www.cnblogs.com/cgzl/p/7788636.html)
      - [IdentityServer4实现Token认证登录以及权限控制](https://www.cnblogs.com/jaycewu/p/7791102.html)
      - [ASP.NET Core 认证与授权[4]:JwtBearer认证 ](https://www.cnblogs.com/RainingNight/p/jwtbearer-authentication-in-asp-net-core.html)
      - [IdentityServer4-从数据库获取User登录并对Claims授权验证（五）](http://www.imooc.com/article/270521?block_id=tuijian_wz)
      - [读取配置文件](https://www.cnblogs.com/Leo_wl/p/5709762.html)
      - [Nuget配置第三方源，缓存目录](https://cloud.tencent.com/developer/article/1342253)
      - [如何用指定端口运行项目](/编程文档/使用指定端口运行项目.md)
      - [EntityFreamework如何设置查询超时](/编程文档/EF设置查询超时.md)
   - ABP
   - Java
      - IDEA部分
         - [IDEA使用教程](https://www.jianshu.com/p/9c65b7613c30)
         - [IDEA下Devtools配置](https://www.cnblogs.com/gmq-sh/p/7727367.html)
         - [IDEA下Maven安装配置](https://www.cnblogs.com/sigm/p/6035155.html)
      - Maven部分
         - [Windows下Maven配置](https://www.cnblogs.com/haimishasha/p/8504421.html)
      - SpringBoot
         - [纯洁的微笑官网](http://www.ityouknow.com)
         - [SpringBoot系列教程](https://www.cnblogs.com/ityouknow/p/5662753.html)
         - [SpringBoot官网-项目创建(类似ABP)](https://start.spring.io)
         - [springboot项目启动后，自动打开默认浏览器](https://blog.csdn.net/superlover_/article/details/88418934)
         - [整合Jpa范例](https://www.cnblogs.com/sam-uncle/p/8819478.html)
         - [Jpa多数据源范例](https://blog.csdn.net/abcwanglinyong/article/details/85924615)
      - 开源项目
         - [Spring平台整合activiti工作流引擎实例](https://github.com/shenzhanwang/Spring-activiti)
      - Activity
         - [手把手教你如何玩转Activiti工作流](https://blog.csdn.net/cs_hnu_scw/article/details/79059965)
         - [如何学习Activit-官网](https://www.activiti.org/userguide/)
         - [在线API文档](https://www.activiti.org/javadocs/index.html)
         - [Activiti进阶（一）--工作流（流程框架）](https://blog.csdn.net/qq_42112846/article/details/81106814)
      - ORM部分
         - [mybatis常用方法](https://blog.csdn.net/mr_chenjie_c/article/details/80068510)
         - [mybatis官网](https://mybatis.org/mybatis-3/zh/index.html)
         - [MybatisPlus官方文档](https://mp.baomidou.com/guide/)
         - [Jfinal文档](http://www.jfinal.com/)
   - Go 
      - [Go的gui库Walk简单使用](https://blog.csdn.net/bw761813/article/details/89673030)
      - [Walk库仓库](https://github.com/lxn/walk)
      - [go语言环境配置](https://blog.csdn.net/u013295518/article/details/78766086)
   - Nodejs
      - [koa2环境搭建](https://blog.csdn.net/weixin_42795831/article/details/82765912)
      - [Koa2开源项目]
   - Python
      - [Python包管理pip如何用上国内镜像](https://www.cnblogs.com/wqpkita/p/7248525.html)
      - [Python pip 国内镜像大全及使用办法](https://blog.csdn.net/madrabbit1987/article/details/81677114)
      - [Python新利器之pipenv](https://www.jianshu.com/p/00af447f0005)
      - [python实现opencv学习一：安装、环境配置、工具](https://blog.csdn.net/u011321546/article/details/79499598)
- 前端语言
   - Vue
      - Vue管理框架收集
         - [Vue-Element-Admin](https://panjiachen.gitee.io/vue-element-admin-site/zh/)
         - [D2Admin](https://d2admin.fairyever.com/#/index) 
         - [飞冰](https://ice.work)
         - [基于Vue+Vuex+iView的电子商城网站](https://github.com/PowerDos) 
         - [Vue资源汇总](https://www.cnblogs.com/zxyzm/p/10651124.html)
      - 其他前端框架
         - [MintUi](https://mint-ui.github.io/docs/#/)
         - [Vant](https://youzan.github.io/vant/#/zh-CN/list)
   - Angular
      - [Ng-alain](https://ng-alain.com/zh)
      - [Ng-zorro-antd](https://ng.ant.design/docs/introduce/zh)
   - React
   - Electron
      - [解决install.js卡死的问题](https://www.jianshu.com/p/eac8f37d6992)

### 免费软件推荐
- [Mysql查询分析器MysqlWorkBench](https://dev.mysql.com/downloads/workbench/)
- [免费的数据库查询工具HeidiSql](https://www.heidisql.com/download.php)
- [Redis可视化工具Fastoredis](https://fastoredis.com/anonim_users_downloads)
- [MongoDb可视化工具Robo3T](https://robomongo.org/download)

### 实战演练
- [在centos7.5环境下配置实现.net core项目的自动化部署](/实战演练/自动化部署/main.md)


### 专项课题(图文教学)
- Win10环境在Hyper-v下安装Centos并运行Docker
   - [win10环境安装Hyper-v虚拟机](/运维文档/在win10操作系统下安装Hyper-v.md)
   - [基于Hyper-v安装Centos7.5](/运维文档/通过Hyper-v安装Centos7.5.md)
   - [Centos7.5常用软件以及Docker的安装](/运维文档/在纯净的Centos7.5下安装常用软件和Docker.md)
   - [Docker常用操作以及容器安装运行](/运维文档/基于Docker安装和运行常用容器.md)

### 技术教程
   - 在线教程
      - [Docker在线教程](https://yeasy.gitbooks.io/docker_practice/content/)
      - [阮一峰的Docker入门教程](http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)
   - 完整版教材
      - [Docker入门到实践，这个强推](https://www.gitbook.com/book/yeasy/docker_practice/details)

---
## 其他内容（未分类）
#### 优秀在线工具分享
- [蓝湖APP——在线产品，设计图，分享标注](https://lanhuapp.com/?home)
- [在线流程图，脑图，设计稿，文件数有上限](https://www.processon.com/)
- draw.io
   - [在线网站](https://www.draw.io/)
   - [开源地址](https://github.com/jgraph/drawio)

<!-- 
#### 软件破解(有条件建议支持正版，或者使用免费的社区版)
- IDEA
   - [IDEA破解1](https://blog.csdn.net/best_luxi/article/details/81479820)
   - [IDEA破解2](https://blog.csdn.net/yl1712725180/article/details/80309862) -->
