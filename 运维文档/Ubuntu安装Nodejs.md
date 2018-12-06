#### Ubuntu怎么安装最新版的Nodejs。npm等


#### 下载解压缩
1. 去官方网站下载最新的软件包，或者用命令wget下载
2. 解压缩：tar zxvf node-xxx.tar.gz 
3. 重命名：mv node-xxx.tar.gz node
4. 移动文件到目录：mv node /usr/local

#### 建立软连接
```
ln -s /usr/loca/node/bin/node /usr/bin/node
ln -s /usr/loca/node/bin/npm /usr/bin/npm
ln -s /usr/loca/node/bin/npx /usr/bin/npx

```
