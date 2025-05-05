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





## 扫描结果说明
SonarQube扫描后会把结果上传到服务器, 会在服务器产生报表, 方便查看哪一行代码出现了哪种问题, 这部分列出来了所有代码存在的问题和缺陷


### Dashboard

### Bugs

### Vulnerabilities

### Security Hotspots

### Debt


### Code Smells


### Unit Test

## SonarQube 其他功能说明
### Issues


### Measures


### Code


### Activity



## 集成Git服务器
SonarQube还可以集成在Git服务器上, 在每次合并代码的时候都进行扫描, 实现自动化处理, 这个本文稍后会给出说明,敬请期待
