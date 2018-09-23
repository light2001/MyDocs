### 本文的目标是在Centos 7.5版本下实现.Net Core部署
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



    主要分为几个步骤
    1. 环境安装
    2. gitlab配置
    3. .Net Core项目配置
    4. 实现自动化部署


### 环境安装
    环境主要分为硬件环境和软件环境：
    一. 硬件环境
    1. 内存至少8g以上，16g更好，因为虚拟机至少需要4g或者更多的内存
    2. CPU在i5即可，没有更多要求
    3. 硬盘至少30g空间，用于安装软件，如果觉得紧张，那15g是必不可少的了

    二. 软件环境
    1. Centos7.5——linux操作系统
    2. Nginx——反向代理
    3. Dcoker——docker容器
    4. Docker-compose——容器编排
    5. Vim——文本编辑器
    6. Firewall——防火墙
    7. Docker下的Gitlab
    8. Gitlab-Runner——自动化部署的客户端软件

    虚拟机我采用的是Vmware，Centos的ISO我是从官网下载的最新版1804，安装后显示centos为7.5版本

#### 安装步骤
1. Centos安装

    虚拟机安装过程比较简单，这里就不展开描述了，只说几个注意点
    1. 安装过程中，软件安装的选项，选择最小安装，所有额外的软件都不安装，这样可以节省资源不说，而且装太多，会占用大量磁盘空间
    2. 安装过程中记得把网卡打开，如果没有打开，可以在装完后，用终端，vi编辑 /etc/sysconfig/network-scripts/ifcfg-ns33 类似这个文件，最后的尾数可能不相同。设置：“ONBOOT=yes”,保存后重启，就会连上网络
    3. 查看当前IP地址 ，centos7.5默认没有ifconfig命令，只能用ip addr查看

2. Windows下SSH软件的选择

    推荐几款终端软件
    1. gitbash,安装好git就会出现，这个终端出奇的好用，就是没有多终端管理之类的强化功能,这个软件是免费的
    2. 如果你的操作系统是win10 ,可以在应用市场安装Ubuntu这个APP，这是一个完整的Linux子系统，可以直接在Power shell里使用它的终端界面
    3. SecureCRT ，老牌终端程序了，不过这个是收费的
    4. Zoc7，本来是Mac下的终端，超好用，目前发现Windows下同样提供了，比以上所的所有终端都好用，也是收费软件

3. Docker的安装
    
    由于有那堵墙在，所以国内的Linux软件下载速度都奇慢无比，所以，需要配置国内的镜像源，这里选择的是阿里的源
    1. 先安装基础软件
    ```
    sudo yum install -y yum-utils device-mapper-persistent-data lvm2
    ```
    2. 配置阿里的镜像
    ```
    sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
    ```
    3. 安装docker
    ```
        sudo yum makecache fast

        sudo yum -y install docker-ce
    ```
    4. 启动docker并设置开机启动
    ```
        sudo systemctl enable docker
        sudo systemctl start docker
    ```
    5. 测试是否安装完毕,执行如下命令，正常会看到结果
    ```
        [root@localhost sysconfig]# docker images
        REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
        gitlab/gitlab-ce    latest              b199bc7f269f        39 hours ago        1.47GB
        [root@localhost sysconfig]#    

    ```
4. 安装docker-compose 
    docker-compose安装比较简单，官方提供了curl地址
    ```
    #安装
    sudo curl -L https://github.com/docker/compose/releases/download/1.17.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose

    #授权命令
    sudo chmod +x /usr/local/bin/docker-compose
    ```
    安装完毕后检验结果：
    ```
    [root@localhost sysconfig]# docker-compose --version
    docker-compose version 1.17.1, build 6d101fb
    [root@localhost sysconfig]# 

    ```
    
5. 安装基于docker的gitlab

    1. 编写docker-compose.yml文件

        为什么要编写docker-compose文件？
        
        这里简单说一下，docker-compose是docker官方提供的容器编排工具，上手比较简单，主要功能就是操作容器，包括容器的下载，运行，关闭，查看状态，等等，容器运行的一些参数，可以直接用docker-compose操作，不用每次都敲docker run xxx命令，docker-compose.yml是docker-compose的模板文件，会根据这个文件，执行一系列的命令，命令结果，默认在docker本地仓库内，和当前所处的目录无关

    先创建目录和文件
    ```
        cd /home
        mkdir gitlab
        cd gitlab
        mkdir docker-compose.yml
        vim docker-compose.yml

    ```
    文件内容：
    ```
    version: '3'

    services:
        gitlab:
            image: gitlab/gitlab-ce
            container_name: "gitlab"
            restart: always
            ports:
            - "8080:80"
            - "443:443"
            - "10022:22"
            environment:
                GITLAB_OMNIBUS_CONFIG: |
                    external_url 'http://gitlab.baidu.com'
                    gitlab_rails['gitlab_shell_ssh_port'] = 10022
            volumes:
            - '/srv/gitlab/config:/etc/gitlab'
            - '/srv/gitlab/logs:/var/log/gitlab'
            - '/srv/gitlab/data:/var/opt/gitlab'
    networks:
    default:
        driver: bridge
    ```
    文件内容不多做解释，简单来说就是下载gitlab/gitlab-ce并运行，映射到主机的端口，注意这一句中的域名，下面的步骤会用到
    ```
        external_url 'http://gitlab.baidu.com
    ```
    2. 运行docker-compose.yml文件

        可以直接敲命令，不过为了不重复劳动，建议创建一个.sh文件，用于执行
        ```
        cd /home/gitlab/docker-compose
        mkdir run.sh
        vim run.sh
        # 文件内容：
        docker-compose up -d --build --force-recreate
        # 使用
        sh run.sh
        ```
        #正常会执行下载gitlab-ce的操作，大概1.6g左右

    至此，一个在docker下运行的gitlab环境就安装完毕了，在环境跟本文一致的情况下，亲测有效，如有意外，自行解决

    
    *注意：以上所有操作，均在root用户下进行，下面也不再重复*
    
    


