### 本文的目标是在Centos 7.5版本下实现.Net Core部署步骤一
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

### 步骤一环境安装

### [步骤二gitlab配置](/实战演练/自动化部署/gitlabSetup.md)

### [步骤三.Net Core项目配置](/实战演练/自动化部署/aspnetcore.md)

### [步骤四实现自动化部署](/实战演练/自动化部署/CICD.md)


---
### 步骤一环境安装
    环境主要分为硬件环境和软件环境：
    一. 硬件环境
    1. 内存至少8g以上，16g更好，因为虚拟机至少需要4g或者更多的内存
    2. CPU在i5即可，没有更多要求
    3. 硬盘至少30g空间，用于安装软件，如果觉得紧张，那15g是必不可少的了
    4. 安装时会安装两台服务器，一台用于gitlab服务器，另一台作为web服务器，这台硬件要求可以放低一点，因为只是测试环境，不存在高并发情况
    5. 我的两台服务器，一台给了单CPU4核心，8G内存40G硬盘，另一台单核单CPU，2G内存20G硬盘
    

    二. 软件环境
    1. Centos7.5——linux操作系统
    2. Nginx——反向代理
    3. Dcoker——docker容器
    4. Docker-compose——容器编排
    5. Vim——文本编辑器，这个安装很简单，就不单独说明了
    6. Firewall——防火墙
    7. Docker下的Gitlab
    8. Gitlab-Runner——自动化部署的客户端软件
    9. .Net CoreSDK的安装

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
    5. SmarTTY，最近才发现的完全免费的ssh，出奇的好用，还免费试用，强烈建议试用
    6. Putty 完全开源免费的，使用起来类似gitbash
    7. Cygwin，这个东东能提供win下的整个linux环境，非常强大，他不仅仅是一个ssh

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
    
6. 配置防火墙

    默认情况下，和以往不同，centos7安装了firewalld，而不是iptables，这个新防火墙我还不清楚好坏，但是操作起来简单多了，所以本次就不换成iptables了
    1. 配置开放80，8080端口
    ```
    firewall-cmd --zone=public --add-port=80/tcp --permanent    （--permanent永久生效，没有此参数重启后失效）
    firewall-cmd --zone=public --add-port=8080/tcp --permanent
    ```
    2. 重新载入
    ```
    firewall-cmd --reload
    ```
    3. 查看是否生效
    ```
    [root@localhost sysconfig]# firewall-cmd --zone=public --query-port=80/tcp
    yes
    [root@localhost sysconfig]# 
    ```
    4. 测试gitlab，看是否已经可用
    
    在宿主电脑，打开浏览器，输入：http://192.168.1.xxx:8080 (需要输入你虚拟机的IP地址)  如下截图所示就表示已经正常了
    
    ![图片](/实战演练/自动化部署/images/gitlablogin.png)

    如果这样，是不是就证明你的gitlab可以用了，不，还不行，因为你的域名是IP地址，并且带有端口，无法正常使用，我们还需要引入Nginx

7. 安装nginx并配置生效

    nginx的作用是端口，域名，路由，等等转发，也非常使用用于静态文件的web服务器，这里只用作域名转发

    1. 安装Nginx
    ```
    # 安装基础软件
    sudo yum install epel-release
    # 安装nginx
    sudo yum install nginx
    ```
    2. 启动nginx
    ```
    sudo systemctl start nginx
    sudo systemctl enable nginx
    ```

    3. 修改nginx的配置文件

        nginx的配置文件分几种，一种是/etc/nginx/nginx.conf，核心配置文件，还有一种属于客户配置的文件，放在/etc/nginx/conf.d/ 这个目录下

        修改nginx.conf，将其中的用户修改为root，这里是为了方便，正常应该建立nginx用户并授权，如截图所示

        ![图片](/实战演练/自动化部署/images/nginxconf.png)

        在/etc/nginx/conf.d下添加一个配置文件
        ```
        [root@localhost nginx]# cd /etc/nginx/conf.d
        [root@localhost conf.d]# ls
        gitlab.conf
        [root@localhost conf.d]# vim gitlab.conf
        # 文件内容：

        server {  
        listen       80;  
        server_name  gitlab.baidu.com;
        access_log  /var/log/nginxhost.access.log  main;  
        location / {  
            proxy_pass   http://127.0.0.1:8080; 
            }       
        }  

        ```
    4. 重新读取nginx配置

        输入命令，让新配置的配置文件生效
        ```
        [root@localhost conf.d]# nginx -s reload
        [root@localhost conf.d]#

        ```

    5. 修改selinux，允许nginx通过

        为什么要做这一步？
        
        因为selinux默认会审核所有的安全策略，nginx默认是不给通过的，需要配置，否则就算nginx是正常运作的，但是还是会看到nginx502错误

        配置命令：
        ```
        yum install policycoreutils-python  
        sudo cat /var/log/audit/audit.log | grep nginx | grep denied | audit2allow -M mynginx 
        semodule -i mynginx.pp 
        ```
        网上有很多种解决办法，但是最多的一种办法就是关闭selinux，为了安全，我不认为关闭是个好办法
    6. 测试nginx是否生效

        配置本地hosts文件，增加规则
        ```
        192.168.20.139  gitlab.baidu.com
        ```

        打开浏览器，输入地址：http://gitlab.baidu.com 看到下图所示，就表示已经全部成功了

        ![图片](/实战演练/自动化部署/images/gitlabbaidu.png)


8. DotNet2.1 SDK环境安装

    1. 导入rpm源
    ```
    sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm
    ```
    2. 更新软件包
    ```
    sudo yum -y update
    ```
    3. 安装SDK
    ```
    sudo yum -y install dotnet-sdk-2.1
    ```
    4. 校验是否安装成功
    ```
    dotnet --version
    ```
9. gitlab-runner的安装

    gitlab-runner是一个工作者程序，用于接受gitlab上版本更新小心，并触发本地自动化部署脚本的执行

    安装步骤来自于[gitlab的官方网站](https://docs.gitlab.com/ee/README.html)

    1. 安装软件
    ```
    # Linux x86-64
    sudo wget -O /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64

    # Linux x86
    sudo wget -O /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-386

    # Linux arm
    sudo wget -O /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-arm


    ```
    2. 授权
    ```
    sudo chmod +x /usr/local/bin/gitlab-runner
    ```


    3. 验证是否安装成功
    ```
    输入：gitlab-runner list

    ```

    由于实际操作需要安装两台centos，1台作为gitlab服务器，另一台作为web服务器用于发布，安装过成大致一样，就不多做赘述了

    至此，环境安装就已经全部结束了，由于篇幅较长，因此拆分成几个步骤了，下面提供了链接
---

### [步骤二gitlab配置](/实战演练/自动化部署/gitlabSetup.md)

### [步骤三.Net Core项目配置](/实战演练/自动化部署/aspnetcore.md)

### [步骤四实现自动化部署](/实战演练/自动化部署/CICD.md)

