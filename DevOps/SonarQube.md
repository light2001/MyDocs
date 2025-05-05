## SonarQube

Sonar 主要实现的功能是检查代码质量, 比如说对于C#来说一共有260条代码规则, 会检测出有缺陷的写法
结合dotcover 扫描 Unit Test能看到代码的覆盖率.
可以设定代码质量基线, 如果不达标的代码可以拒绝合并

### 运行环境
我的Linux环境是Arch Linux, 本文所检查的语言是以C#为主, 所以以下的一些说明, 都是以Arch Linux和.Net 环境为主

#### Docker
Docker是什么本文不再赘述了, 当前文档的Sonar Server使用的环境就是在Docker里, 因为方便管理, 部署快速.
基于下面的Docker-Compose文档, 不到半小时就能启动一个完整的SonarQube Server环境了

#### Docker-Compose
Docker-Compsoe是用来编排Docker容器的, 所以必须安装以下, 下面给出安装方法

```shell
sudo pacman -S docker-compose
```
查看是否安装成功:
```shell
docker-compose --version
```


#### Java环境
Java环境主要是用于Sonar Scanner这个扫描工具的, 由于Arch Linux自带了OpenJDK环境,所以这里不再赘述

#### .Net SDK
由于用的项目是.Net的项目, 所以这里的基础代码运行环境也是以.Net SDK为主
如何安装环境? 使用下面的代码会安装最新版的9.0

```shell
sudo pacman -S dotnet-sdk
```
查看是否安装成功:
```shell
dotnet --version
```


## SonqrQube Server

SonarQube有Cloud版本,和本地化部署的版本,可以查看官网的价格页面, 查看他们的区别,对于个人开发者是免费使用的
对于小团队的话, 价格看起来还可以, 当然也可以直接使用开源版本


### 下面是docker compose ,通过这个脚本就能一键启动SonarQube的Docker容器
```YAML
version: "3"

services:
  # SonarQube Database Service
  db:
    image: postgres:15 # Use a specific stable version like 15
    container_name: sonarqube_db
    environment:
      # !!! IMPORTANT: Change these default values for security !!!
      POSTGRES_USER: sonarqube
      POSTGRES_PASSWORD: Abc123456 # <-- CHANGE THIS PASSWORD
      POSTGRES_DB: sonarqube
    volumes:
      - db_data:/var/lib/postgresql/data # Persist database data
    restart: unless-stopped # Auto-restart unless explicitly stopped

  # SonarQube Application Service
  sonarqube:
    image: sonarqube:lts # Use the Long Term Support (LTS) version
    container_name: sonarqube_app
    ports:
      - "9000:9000" # Map host port 9000 to SonarQube container port 9000
    environment:
      # Configure SonarQube to connect to the PostgreSQL database
      # jdbc:postgresql://<db_service_name>:<db_port>/<db_name>
      SONARQUBE_JDBC_URL: jdbc:postgresql://db:5432/sonarqube
      # !!! IMPORTANT: Use the same user and password as the database service !!!
      SONARQUBE_JDBC_USERNAME: sonarqube
      SONARQUBE_JDBC_PASSWORD: Abc123456 # <-- USE THE SAME PASSWORD
      # Configure Elasticsearch memory for SonarQube (adjust based on your resources)
      # Minimum 2GB RAM is generally recommended for SonarQube
      SONAR_SEARCH_JAVA_OPTS: "-Xmx1024m -Xms1024m -XX:+HeapDumpOnOutOfMemoryError" # Example: 1GB heap
    volumes:
      - sonarqube_data:/opt/sonarqube/data # Persist SonarQube data
      - sonarqube_extensions:/opt/sonarqube/extensions # Persist plugins and extensions
      - sonarqube_logs:/opt/sonarqube/logs # Persist logs
    depends_on:
      - db # Ensure database starts before SonarQube
    restart: unless-stopped

# Define named volumes for data persistence
volumes:
  db_data:
  sonarqube_data:
  sonarqube_extensions:
  sonarqube_logs:

```
创建一个新的目录, 把上面的文件保存为yml格式的文件, 文件名: docker-compose.yml

如下面截图所示
![image](https://github.com/user-attachments/assets/8abfd86a-9be9-44ee-869f-f8953c83bb13)


### 如何运行?
在终端敲下面的命令即可, 这个命令会自动查找当前目录的"docker-compose.yml"文件,并下载镜像和运行容器

```shell
docker-compose up -d
```
执行后会看到自动下载了docker相关的镜像
![image](https://github.com/user-attachments/assets/6dc06104-c8fe-4f23-970d-6b2726143ba8)


下面是Docker容器已经运行起来的截图
![image](https://github.com/user-attachments/assets/017e8079-af10-4240-9ded-6a82561ff6dc)


### 默认的账号密码:
运行成功后,你会发现打开了登陆界面, 但是你不知道账号和密码, 如下图所示:
![image](https://github.com/user-attachments/assets/ed223e71-e7f2-4e2f-9bb9-d42ffaa36c09)
SonarQube的默认账号密码如下:

```
账号: admin
密码: admin
```



## Sonar Lint
Sonar lint的作用是在IDE开发环境里扫描代码存在的问题,它是以IDE的插件形式存在的.
如果您购买了SonarQube的Cloud服务或者购买了企业版本地化部署, 那么就可以开启这个功能了.
这个功能其实和Rider, VisualStudio的代码提示有一些冲突, 可以用用看, 但是不推荐, 这里不多做介绍

这个插件现在现在已经改名为：SonarQube For IDE, 如下图所示
![image](https://github.com/user-attachments/assets/c159e1da-2260-4edb-b7bc-241491a40eb3)




## Sonar Scanner
Sonar Scanner是用来扫描代码质量, 扫描Unit Test ,扫描结束以后, 会把报告上传到指定的SonarQube服务器上

### 安装Sonar Scanner

想要正常扫描的话,必须安装SonarScanner, 这个软件可以通过dotnet tool这个工具安装, 下面给出了安装命令, 非常简单

```shell
dotnet tool install --global dotnet-sonarscanner
```
设置dotnet tool的环境变量, 否则无法执行

```shell
nano ~/.bashrc
# 或者使用 vim
# vim ~/.bashrc

# Add dotnet tools to PATH
export PATH="$PATH:$HOME/.dotnet/tools"

# load env
source ~/.bashrc
```

如果你使用的是ZSH 的话, 需要修改~/.zshrc ,这里不再赘述了

### Project设置
SonarQube是以目录为单位工作的, 需要在SonarQube里创建一个项目,所以这里必须先配置项目
![image](https://github.com/user-attachments/assets/2c925747-0a63-4c47-978a-64ec363d48fc)

设置完项目以后,会给到一个Project token, 不是必须用这个凭据来上传项目, 也可以使用User Token

Project Token : 
```shell
sqp_54ece4e750e93af9b97cb293eaed254bdb81554b
```

Project Name: TestProject


### 扫描项目

```shell
dotnet sonarscanner begin /k:"TestProject" /d:sonar.host.url="http://192.168.170.128:9000"  /d:sonar.login="sqp_54ece4e750e93af9b97cb293eaed254bdb81554b"
dotnet build
dotnet sonarscanner end /d:sonar.login="sqp_54ece4e750e93af9b97cb293eaed254bdb81554b"
```
</br>
</br>
</br>
</br>
</br>

# 如何查看和分析扫描结果

## [SonarQube的结果如何分析](SonarQubeUse.md)
