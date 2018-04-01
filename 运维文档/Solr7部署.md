### Solr7.2.1在windows环境，部署在tomcat下，连接MSSQL数据库

首先根据看下面这篇文档可以解决90%的问题
<a href="https://www.cnblogs.com/itdragon/p/7995040.html" target="_blank">Solr7.2部署</>

但是仍然有一些问题没有说明，比如连接MSSQL应该怎么处理
Sqlserver的连接方式是，如果是用JDBC，必须去下载JDBC的驱动程序，sqljdbc4.jar或者更高版本
然后复制到 tomcat/webapps/solr/WEB-INF/lib 目录下，否则就会无法连接数据库