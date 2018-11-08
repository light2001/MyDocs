### 本文档是工作中常见Git问题收集
主要内容如下：
1. git强制拉取代码
2. git从远程仓库拉取代码到本地
3. git切换远程仓库到本地



#### 分类文档
1. git强制拉取远程代码，覆盖本地代码
```
git fetch --all  
git reset --hard origin/master 
git pull
```

2. git从远程仓库拉取代码到本地
```
git clone http://UserName:Password@github.com/light2001/MyDocs.git

注意： 
如果用户或者密码中有"@"符号，则需要用 "%40" 代替，否则会报密码错误
```

3. git切换远程仓库到本地

通过
```
git checkout -b 
```
创建本地分支，同时制定远程仓库名，会自动建立链接，好处是以后可以直接用git pull拉取代码
```
git checkout -b dev origin/dev
```

如果远程仓库无法识别，则需要麻烦一点的步骤
```
git fetch origin 远程分支名x:本地分支名x
```
这样存在的问题是，需要自己手动 
```
git checkout branch
```
切换分支，然后用
```
git branch -u origin/远程分支 
```
建立链接