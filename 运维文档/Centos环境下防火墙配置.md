#### CENTOS 下安装防火墙


根据以下这篇教程配置

<a href="https://www.linuxidc.com/Linux/2017-01/139622.htm" target="_blank">Iptables安装教程<a/>



<a href="https://blog.csdn.net/irokay/article/details/72717132" target="_blank">Centos关闭默认防火墙，开启Iptables<a/>

<a href="https://www.cnblogs.com/hubing/p/6058932.html" target="_blank">Centos firewall防火墙详解</a>

#### firewalld使用简介
```
怎么开启一个端口
添加
firewall-cmd --zone=public --add-port=80/tcp --permanent    （--permanent永久生效，没有此参数重启后失效）
重新载入
firewall-cmd --reload
查看
firewall-cmd --zone=public --query-port=80/tcp
删除
firewall-cmd --zone=public --remove-port=80/tcp --permanent

```