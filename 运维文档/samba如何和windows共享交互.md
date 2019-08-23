#### 本文介绍samba-client如何和windows目录交互

背景介绍：
    
    本文基于Centos7.6环境下操作，内容是，从linux的samba客户端，连接到windows的共享目录，并实现开机自动挂载

#### 先安装软件
```
# 挂载目录用的
yum -y install cifs-utils

# samba的客户端软件
yum -y install samba-client

```


#### 然后连接目录
```
smbclient  //192.168.8.20/foldername -U DomainName/username%password

# 连接后可以用ls等命令查看目录下的内容，退出请输入:

exit

```

#### 挂载目录到指定目录下，需要权限
```

sudo mount.cifs -o user="username",pass="password",dom="domainname"  //192.168.8.20/gcs /mnt/foldername


```

#### 断开目录

```
umount /mnt/foldername

```


#### 设置开机就挂载

```
# 编辑/etc/fstab文件，在里面增加一行内容,就会实现开机就加载
vim /etc/fstab 

mount.cifs -o user="username",pass="password",dom="domainname"  //192.168.8.20/gcs /mnt/foldername

```