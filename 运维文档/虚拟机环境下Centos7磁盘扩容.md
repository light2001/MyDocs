#### Hyper-v虚拟机环境下的Centos7磁盘扩容

[Hyper-v下Centos7使用LVM实现动态扩容磁盘](http://www.apoyl.com/?p=2232)

其中还缺关键的一部
在磁盘创建好以后，必须运行以下命令,pvcreate /dev/sda3 才会认

```
mkfs.ext4 /dev/sdf3

```