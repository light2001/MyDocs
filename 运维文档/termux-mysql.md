#### 前提条件
  
    事先安装好vim等文本编辑工具

#### 安装步骤
- 安装服务器端软件

##### 搜索数据库软件，查看是否存在

~~~
pkg search mysql
~~~
如图所示，termux上只能看到mariadb，没有mysql，不过使用起来是一样的
  ![image](https://github.com/light2001/MyDocs/assets/3821091/5c2b42ec-63e4-4c27-9c3e-906fbd46c76f)


##### 安装软件
~~~
pkg install mariadb
~~~
- 调整配置文件
~~~
cd /data/data/com.termux/files/usr/etc
nvim my.cnf

# 我的配置如下：
[mysqld]
init-connect='SET NAMES utf8mb4'
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
[client]
default-character-set=utf8mb4

!includedir /data/data/com.termux/files/usr/etc/my.cnf.d
~~~

- 启动数据库服务
~~~
mysqld_safe -u root &
~~~
查看是否启动成功：
~~~
ps -ef | grep mysqld
~~~
![image](https://github.com/light2001/MyDocs/assets/3821091/347c3e6e-396c-498d-bafe-0dca03475b4e)

- 客户端连接
- 创建数据库
- 导入数据
  
