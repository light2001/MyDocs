### 扩充硬盘

-   查看硬盘的设备名
-   格式化硬盘
-   挂载
-   重启，查看

#### 查看硬盘的设备名

>两种方式都可以
>fdisk -l //或者cat /proc/partitions 


#### 新建分区

>有些人会在这里新建分区 但是由于本人的硬盘是 希捷4T SSD
>所以我在这里也提供新建分区的方法
>fdisk /dev/sdb //这里的sdb是新添加出来的硬盘
>
>n //添加新分区 
>
>p //创建主分区 
>
>1 分区号1 
>
>按回车 //起始扇区选择默认 
>
>也是回车默认 //为了不浪费空间
> 
>p //查看创建出来的分区 
>
>w //保存
>

#### 格式化硬盘

>mkfs.ext4 /dev/sdb  //或者mkfs -t ext4 /dev/sdb
>


#### 挂载硬盘

>vim /etc/fstab  进入文件编辑
>
>File&fstab
>
>/dev/sdb /newdisk  ext4 defaults 0 0


| 硬盘 | 位置 |  格式 | 默认| 
|---|---|--- |----|
|/dev/sdb1 | /mnt/daobin | ext4 | defaults 0 0 |

#### 重启，查看 
>reboot 
>
> df -h  
>如果有你所操作的那个硬盘则挂载成功 

