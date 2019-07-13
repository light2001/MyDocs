#### Hyper-v虚拟机环境下的Centos7磁盘扩容

首先参考下面的文章：


[Hyper-v下Centos7使用LVM实现动态扩容磁盘](http://www.apoyl.com/?p=2232)
[阿里云对应教程-扩展分区和文件系统_Linux系统盘](https://help.aliyun.com/document_detail/111738.html?spm=a2c4g.11186623.4.2.6c297f67raZJ60)

其中还缺关键的一部
在磁盘创建好以后，必须运行以下命令,pvcreate /dev/sda3 才会认

```
mkfs.ext4 /dev/sdf3

```