### Docker日志容量限制总容量

#### 背景介绍
在我们使用Docker容器启动服务时，常常会由于容器内的日志过多导致把宿主机的磁盘打满。
本文主要讲解如何解决容器日志打满磁盘的问题。

#### 容器日志目录

首先，我们来讲一下容器日志的位置。如果你的磁盘已经被容器日志所打满，则需要找到对应的日志并进行删除。

默认情况下，每个容器的日志默认都会以json-file的格式存储于

```
 /var/lib/docker/containers/&lt;容器id>/&lt;容器id>-json.log文件中。
```

如果你的磁盘已经被日志打满，此时可以清除该文件来释放空间。需要注意的是，不建议直接使用rm命令删除日志文件，因为在某些情况下，rm命令无法直接释放磁盘空间。

一种推荐的删除方式如下：
```
  echo " " > /var/lib/docker/containers/&lt;容器id>/&lt;容器id>-json.log
```

上述方法总是治标不治本。为了解决该问题，我们希望能直接限制容器日志的大小。

#### 限制容器日志的方式分为全局限制和单个容器限制。

#### 全局限制

创建/修改/etc/docker/daemon.json该文件，在该文件中增加如下配置：
```
{
  "log-driver":"json-file",
  "log-opts":{ "max-size" :"1g","max-file":"1"}
}

```
此时，表示全局限制所有容器的默认日志配置为json-file格式且最大限制为1G。

#### 单个容器限制

##### docker容器启动命令中配置日志信息

有时，我们希望仅仅针对单个容器进行限制，那么此时方式如下： 
在docker run的容器启动命令中添加如下参数：
```
--log-opt max-size=1g --log-opt max-file=1
```
##### compose文件中配置日志信息
很多时候，我们启动容器不是通过docker run进行挨个启动，而是通过compose进行统一的管理。 
此时，我们同样可以在compose的配置文件中进行容器日志的限制。

一个示例如下：
```
  version: "2"
  services:
    mysql:
      image: mysql
      logging:
        driver: "json-file"
        options:
          max-size: "1g"
```

配置完毕必须重启动Docker
```
  sudo systemctl restart docker

```


#### 真实案例：
时间：2019年6月24
现象描述：

  存放测试环境，gitlab，禅道的服务器磁盘空间满。
  迫于无奈，查找原因，隐约也知道是什么情况，因为gitlab给我的感觉就是会特别占用磁盘空间

解决步骤：
- 输入命令：
```
du -h -x --max-depth=1
```
- 根据返回结果，层层查找，最终定位到 /var/lib/docker/containers/ 目录下， 这个目录是存放docker容器本身资料的地方
- 在这个目录输入上面的命令，会发现某个目录容量特别大，经比对，发现就是gitlab的对应目录，进入目录后，发现json.log日志居然有33g
- 删除文件后，重启docker服务，问题得到解决

经验总结：

  大家在使用Gitlab的时候一定要注意限制他的日志大小，本人所使用的gitlab，总共使用时间大概9个月左右，就有33g这么大的日志，可见还是有必要限制一下的
    

---
#### 本文引用来源地址：
[Docker容器日志打满机器的解决方式](https://www.missshi.cn/api/view/blog/5c4c18a8c7e01951d5000001)

