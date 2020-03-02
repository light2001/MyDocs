#### 如何安装ELK

  基于Docker下安装ELK服务器

#### 参考文档
[CSDN连接：https://blog.csdn.net/qq1031893936/article/details/93798646](https://blog.csdn.net/qq1031893936/article/details/93798646)

#### 其他说明

  Elasticsearch 已经更新到了7.6.0，如果用docker pull 默认版本不是最新的，必须在后面增加版本号才能下载最新版本

  因此，Kibana对应版本也需要下载7.6.0版本才可以正常使用

  例如：
  ~~~
  docker pull elasticsearch:7.6.0
  docker pull kibana:7.6.0
  ~~~

  由于我的Dicker卷文件放在D盘，这里记录下我的Kibana运行语句

  ~~~
  docker run -di --name=mykibana -p 5601:5601 -v /d/Hyper-v/Docker/kibana/config:/usr/share/kibana/config kibana
  ~~~