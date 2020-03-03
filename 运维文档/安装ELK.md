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

  这里要特别说明下，文章里Elasticsearch的IK分词器由于墙的存在是无法安装的，必须手动下载zip文件并解压缩后，然后复制到elasrarch/plugins/ 目录下，并将目录改名为：analysis-ik，并且使用elasticsearch-plugin list能查询到即可

  也可以安装 smart-cn分词器，安装方法：

  ~~~
  cd /usr/share/elasticsearch/bin
  elasticsearch-plugin install smart-cn
  ~~~

  由于我的Dicker卷文件放在D盘，这里记录下我的Kibana运行语句

  ~~~
  docker run -di --name=mykibana -p 5601:5601 -v /d/Hyper-v/Docker/kibana/config:/usr/share/kibana/config kibana
  ~~~

  下面是Logstash的运行语句

  ~~~
  docker run -di --name=mylogstash -v /d/Hyper-v/Docker/logstash/config:/usr/share/logstash/config -v /d/Hyper-v/Docker/logstash/pipeline:/usr/share/logstash/pipeline logstash:7.6.0
  ~~~