# SonarQube怎么使用
上一篇主要讲了Sonar是怎么安装运行的, 这一篇主要讲怎么使用

## 配置项目
SonarQube是以项目为单位运行的,所以要先配置项目, 然后基于项目的地址去扫描并上传结果
下面以本地项目为例, 说明一下怎么配置本地的项目, 不集成git服务器

### 创建项目
点击下图所示的 创建项目图标, 就会打开创建项目界面
![image](https://github.com/user-attachments/assets/028e497d-dbd8-4435-a1a2-e4bf4610d2f9)

选择创建项目的目标
![image](https://github.com/user-attachments/assets/8558cda5-9add-4600-8edc-d2a9a3207ee4)
这张图可以看到, 其实可以直接集成git服务器的,不过这里先用本地来处理

给项目取名CoreShop
![image](https://github.com/user-attachments/assets/afc9e962-78ce-41b1-b536-a6481171593e)

这一步是问你是否要集成CI
![image](https://github.com/user-attachments/assets/6f5c1c3e-e0a9-4ed6-b409-ba99919d6dfc)

这个界面会问你怎么创建访问的project 级别的token
![image](https://github.com/user-attachments/assets/12ffb224-06a0-4301-80cf-0ceecd9a16a4)

这一步需要记录生成后的token, 这个token是项目级别的, 只能用在这个项目上,不能在其他项目使用
![image](https://github.com/user-attachments/assets/cac57cec-afae-45de-836e-15be790765f9)

```
sqp_c88167212d842c08915f951614e96cb942e95fb2
```

这一步是选择一个开发语言, 对应你项目的语言就好
![image](https://github.com/user-attachments/assets/50422c23-c7c6-4c98-8b20-175d8413c6cc)

下面是选择了.Net后的结果, 这里会展示怎么扫描.Net项目
![image](https://github.com/user-attachments/assets/26272b1f-7ef0-42f6-856f-63e9dfbab8fe)

设置好项目以后, 在主界面就能看到有两个项目了,可以看到新创建的项目目前没有结果, 因为还没有扫描
![image](https://github.com/user-attachments/assets/bd637b2c-54a3-4026-8592-c65cf8627688)




## 扫描结果说明
SonarQube扫描后会把结果上传到服务器, 会在服务器产生报表, 方便查看哪一行代码出现了哪种问题, 这部分列出来了所有代码存在的问题和缺陷
下面会展开说明

### Dashboard
在项目页面可以看到多个项目的简单预览
![image](https://github.com/user-attachments/assets/597b81d8-23cb-444b-b648-3d7d14b5fb6d)

下图可以看到一个项目的扫描结果
![image](https://github.com/user-attachments/assets/41bd16ad-f9d2-4824-b009-484e360a2152)
这里可以看到下列信息:
- Bugs
- Vulnerabilities
- Security Hotspots
- Debt
- Code Smells
- Unit Tests converage
- Duplications



### Bugs
这个问题叫做Bugs是因为可能造成Bug,有安全隐患在

下面是bugs的详细信息
![image](https://github.com/user-attachments/assets/5492aa9d-3ce2-449e-9435-db7b1d2935ac)

如果打开第一个错误, 就能看到具体的信息:
![image](https://github.com/user-attachments/assets/1fa44f06-ee9a-42ed-b0c9-3c0ea310d34c)
这里的问题是: 划线的变量, 始终不为空,所以等式不成立

这里可以过滤不同的数据:
- Bug
- Vulnerability
- Code Smell
![image](https://github.com/user-attachments/assets/dde0e339-3915-4950-9f39-a41bd31e0e39)

这里可以过滤语言,通过下图可以看到,其实大部分问题都是前端Web页面造成的
![image](https://github.com/user-attachments/assets/0f6340d0-23ea-47bd-ab79-2d088843ae6f)

过滤后的Bugs只有16个了
![image](https://github.com/user-attachments/assets/80e72f0a-2e2d-42de-a8c3-8e0f99776bf5)



### Vulnerabilities
这个分类可以叫做缺陷或者漏洞, 也是比较严重的问题,不过用来测试的项目目前没有问题


### Security Hotspots
这个分类叫做安全热点,可以看到都是和安全有关的问题
![image](https://github.com/user-attachments/assets/c1929b5e-ec36-40e2-bb0e-1404f5f3b43c)

比如不安全的随机数
![image](https://github.com/user-attachments/assets/7959ee62-d3e2-43dd-bd4c-36a0b3b2ea37)



### Debt
技术债务指的是在开发过程中,由于各种原因导致的代码质量,缺陷, 漏洞, 硬编码等等不好的代码,汇总起来都叫做技术债务
![image](https://github.com/user-attachments/assets/d8027a90-83b8-4986-8f5c-6ebc20663d85)
这里列出了修复当前文件,需要花费的时间, 还是比较靠谱的计算


### Code Smells
这块是SonarQube的比较重点的功能了, 这里主要包括了下面几类问题:
![image](https://github.com/user-attachments/assets/5c2b179f-8ba0-4cd1-ab4b-33c57e158e68)
具体的解说这里就不重复了, SonarQube官网有详细的说明


### Unit Test

单元测试覆盖率也是一个重要的指标, 在外企会比较看重, 国内企业不一定会在意
![image](https://github.com/user-attachments/assets/08c8e05d-cf28-46bc-a75f-542215c0c30d)


## SonarQube 其他功能说明
### Issues
这个界面就是一个查询界面, 所有的问题都汇总在这里
![image](https://github.com/user-attachments/assets/7030ba2e-895f-4b7c-bad8-72ef6c8bc8c3)
可以review问题, 标记已解决, 筛选开发语言, 等等


### Measures
这个界面主要是一些计算,指标等,可以根据多次扫描结果出分析图
![image](https://github.com/user-attachments/assets/f54a539b-e38d-40ae-9138-f2c0fa72954a)

这里可以看到大文件的管理, 如果一个文件行数过多,这里就会提示
![image](https://github.com/user-attachments/assets/d228bf66-b87f-4eb9-ab1c-b96382ab85a3)


### Code
这个界面是以代码文件角度展开的
![image](https://github.com/user-attachments/assets/797499b5-4749-4cfd-9b21-7bd3c320f657)


### Project Settings

这个界面特别说明下, 当前项目的所有扫描活动, 在这个界面都可以看到
![image](https://github.com/user-attachments/assets/20a5eac9-ad37-445e-9ad5-095ad4dbaec6)


### Activity
这个界面是活动记录, 包括所有的扫描活动
![image](https://github.com/user-attachments/assets/f3f16116-6bb2-42ea-86da-d8982ffa3502)



## 集成Git服务器
SonarQube还可以集成在Git服务器上, 在每次合并代码的时候都进行扫描, 实现自动化处理, 这个本文稍后会给出说明,敬请期待
