#### 如果你有两个账号，怎么配置不同的目录使用不同的账号推送


  首先你可以设置全局账号，比如公司的账号设置成全局的，然后某个目录，你可以使用local本地的配置，这样就能区分开不同目录使用不同的账号


#### 本地设置
- 怎么设置设置本地的账号密码

  先设置账号相关，由于git对配置文件，分几个等级
  - local 最高
  - system 最低
  - global 次高
    
  ~~~
  git config --local user.name = light2001
  git config --local user.email = 332976194@qq.com
  git config --local credential.helper store
  ~~~
  
  这时候可以查看一下是否配置到位：
  ~~~
    git config --local --list
  ~~~

- 设置当前目录的账号密码，设置后会存在 ~/.git-credentials 文件里，以加密方式存储
  ~~~
  git config --local credential.https://github.com.username <your_username>
  ~~~

  参考：https://www.baeldung.com/ops/git-configure-credentials

- 查看.git-credential

    ![image](https://github.com/light2001/MyDocs/assets/3821091/aafa77e7-1eee-47c2-bdd4-0b590eb73629)
    
    可以看到有好不同的记录

- 推送时输入账号密码
~~~
 git push 
~~~

  这时候会弹出git 密钥管理，可以选择打开webbrowser，之后就可以正常使用了 




- 存在的问题：

   目前发现如果一个账号，对同一个网站存在两个账号，在pull或者push的时候，会触发弹出 GCM 选择账号的情况，暂时还没找到解决方案

   <span style="color:red;">已经知道怎么解决了，只要设置了全局的默认账号，就不会再提示让你选择账号去pull/push代码了</span>

<code style="color:green;"> test </code>