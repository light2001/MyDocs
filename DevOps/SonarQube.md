## SonarQube

    Sonar 主要实现的功能是, 检查代码质量, 对于C#来说一共有260条代码规则, 会检测出有缺陷的写法
    结合Unit Test能看到代码的覆盖率.
    可以设定代码质量基线, 如果不达标的代码可以拒绝合并

### 运行环境
我的Linux环境是Arch Linux, 本文所检查的语言是以C#为主, 所以以下的一些说明, 都是以Arch Linux和.Net 环境为主

#### Docker
Docker是什么本文不再赘述了, 当前文档的Sonar Server使用的环境就是在Docker里, 因为方便管理, 部署快速.
基于下面的Docker-Compose文档, 不到半小时就能启动一个完整的SonarQube Server环境了

#### Docker-Compose
Docker-Compsoe是用来编排Docker容器的, 所以必须安装以下, 下面给出安装方法

~~~
sudo pacman -S docker-compose
~~~
查看是否安装成功:
~~~
docker-compose --version
~~~


#### Java环境
Java环境主要是用于Sonar Scanner这个扫描工具的, 由于Arch Linux自带了OpenJDK环境,所以这里不再赘述

#### .Net SDK
由于用的项目是.Net的项目, 所以这里的基础代码运行环境也是以.Net SDK为主
如何安装环境? 使用下面的代码会安装最新版的9.0

~~~
sudo pacman -S dotnet-sdk
~~~
查看是否安装成功:
~~~
dotnet --version
~~~


## SonqrQube Server

    SonarQube有Cloud版本,和本地化部署的版本,可以查看官网的价格页面, 查看他们的区别,对于个人开发者是免费使用的
    对于小团队的话, 价格看起来还可以, 当然也可以直接使用开源版本


## 下面是docker compose ,通过这个脚本就能一键启动SonarQube的Docker容器
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

### Project设置
Project Token : 
```shell
sqp_54ece4e750e93af9b97cb293eaed254bdb81554b
```

Project Name: TestProject




## Sonar Lint
Sonar lint的作用是在IDE开发环境里扫描代码存在的问题,它是以IDE的插件形式存在的.
如果您购买了SonarQube的Cloud服务或者购买了企业版本地化部署, 那么就可以开启这个功能了.
这个功能其实和Rider, VisualStudio的代码提示有一些冲突, 可以用用看, 但是不推荐, 这里不多做介绍

这个插件现在现在已经改名为：SonarQube For IDE, 如下图所示
![image](https://github.com/user-attachments/assets/c159e1da-2260-4edb-b7bc-241491a40eb3)


## Sonar Scanner
Sonar Scanner是用来扫描代码质量, 扫描Unit Test ,扫描结束以后, 会把报告上传到指定的SonarQube服务器上

### 安装Sonar Scanner
#### 怎么安装Sonar Scanner:

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

### 扫描项目
```
dotnet sonarscanner begin /k:"TestProject" /d:sonar.host.url="http://192.168.170.128:9000"  /d:sonar.login="sqp_54ece4e750e93af9b97cb293eaed254bdb81554b"
dotnet build
dotnet sonarscanner end /d:sonar.login="sqp_54ece4e750e93af9b97cb293eaed254bdb81554b"
```


## 扫描结果说明
SonarQube扫描后会把结果上传到服务器, 会在服务器产生报表, 方便查看哪一行代码出现了哪种问题,下面展开来说明

### Dashboard

### Bugs

### Vulnerabilities

### Security Hotspots

### Debt


### Code Smells


### Unit Test

## SonarQube 其他功能说明
### Issues


### Measures


### Code


### Activity



## 集成Git服务器
SonarQube还可以集成在Git服务器上, 在每次合并代码的时候都进行扫描, 实现自动化处理, 这个本文稍后会给出说明,敬请期待
