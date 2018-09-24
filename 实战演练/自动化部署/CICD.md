### 本文的目标是在Centos 7.5版本下实现.Net Core部署步骤二


---
背景知识：
    
    本文的目的在于，在Centos环境下，安装gitlab代码管理器，并配合gitlab-runner实现自动化部署，前后端项目均可
    这次选择的是.Net Core后端项目

    想要实现这个目标，需要掌握以下基本知识
    1. Centos基本操作，linux常用命令
    2. Git代码管理知识，常用命令
    3. docker基础知识，docker-compose基础
    4. nginx基础理论，配置文件相关知识
    5. gitlab管理知识，基础操作


---



由于篇幅较长，因此拆分为几篇文章：

### [步骤一环境安装](/实战演练/自动化部署/main.md)

### [步骤二gitlab配置](/实战演练/自动化部署/gitlabSetup.md)

### [步骤三.Net Core项目配置](/实战演练/自动化部署/aspnetcore.md)

### 步骤四实现自动化部署
---
### 步骤四实现CICD自动化部署

    1. CICD背景知识

        CICD的意思是持续部署，持续集成，在开发过程中，经常会合并代码，并发布，在集中开发的过程中，一天会部署N次，如果多人参与同一个项目，发布次数会更多，团队越大，同一个项目参与人数越多，持续部署就越重要

    2. gitlab-runner介绍
        gitlab-runner可以理解为安装在被部署机器上的一个工作者软件，gitlab在目标版本合并的时候会根据当前部署的脚本，触发相应的runner去运行一系列的脚本，脚本由使用者自己定制

        官网最新的文档已经全部都换成gitlab-runner,网上的资料大多都还是gitlab-mutiple-ci-runner的，这是老版本的runner，是否可用没有多做研究

        gitlab-runner根据需要可以分为:
        - 共享
        - 分组
        - 项目独有

        从本质上来看并没有什么区别，只是使用上会有不同，比如共享型的就是一个runner可以给所有项目使用，而分组的runner只能给对应分组的runner使用，我只使用过项目，分组，这两种类型的runner，有兴趣的朋友可以去测试其他类型，然后来给我分享

    3. gitlab-runner使用

        gitlab-runner需要先注册才能使用















---
### [步骤一环境安装](/实战演练/自动化部署/main.md)

### [步骤二gitlab配置](/实战演练/自动化部署/gitlabSetup.md)

### [步骤三.Net Core项目配置](/实战演练/自动化部署/aspnetcore.md)
