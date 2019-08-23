#### 本文介绍samba-client如何和windows目录交互


#### 先安装软件
```

yum -y install cifs-utils


yum -y install samba-client
```


#### 然后连接目录
```
smbclient  //192.168.8.20/foldername -U DomainName/username%password

```

#### 挂载在目录
```

sudo mount.cifs -o user="username",pass="password",dom="domainname"  //192.168.8.20/gcs /mnt/foldername


```

#### 断开目录

```
umount /mnt/foldername

```


#### 设置开机就挂载

```


```