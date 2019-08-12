#### Centos环境下，如何使用tcpdump分析网络流量

####  如何安装
```
yum install -y tcpdump 
```

#### 使用：

```

tcpdump dst 192.168.0.33 -s 0 -c 100 -w /home/target.cap

```

#### 参考资料：
- [CentOS中使用tcpdump抓包](https://www.cnblogs.com/hongdada/p/10565898.html)
- [抓包总结](https://www.cnblogs.com/chenpingzhao/p/9108570.html)
- [Tcpdump命令的使用与示例](https://www.iteblog.com/tcpdump_usage/)
- [Linux tcpdump命令](https://www.runoob.com/linux/linux-comm-tcpdump.html)