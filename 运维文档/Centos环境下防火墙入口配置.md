#### 本文来源于linux公社


根据以下这篇教程配置

<a href="https://www.linuxidc.com/Linux/2017-01/139622.htm" target="_blank">安装教程<a/>
<a href="https://blog.csdn.net/irokay/article/details/72717132" target="_blank">防火墙安装<a/>


https://blog.csdn.net/lee528066/article/details/52947980




#### 关于centos 7 中service iptables save 指令使用失败的结局方案  
    
在刚买的ceno 7服务器中安装vsftpd之后想打开防火墙端口  结果/etc/sysconfig/目录下没有iptables文件  这时候就需要自己写一个iptables文件并且写入相关指令  然后使用 service iptables save 时显示 The service command supports only basic LSB actions (start, stop, restart, try-restart, reload, force-reload, status). For other actions, please try to use systemctl.
百思不得其解，然后上网百度之后，找到了解决方法：
首先不管防火墙有没有关 都使用systemctl stop firewalld 关闭防火墙
然后使用 yum install iptables-services 安装或更新服务
再使用systemctl enable iptables 启动iptables
最后 systemctl start iptables 打开iptables
大功告成
试试service iptables save
