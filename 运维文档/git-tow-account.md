#### 如果你有两个账号，怎么配置不同的目录使用不同的账号推送


#### 本地设置
- 设置本地的账号密码

  先设置账号相关，由于git分几个等级
  - local 最高
  - system 最低
  - global 次高
  ~~~
  git config --local user.name = light2001
  git config --local user.email = 332976194@qq.com
  git config --local credential.helper store
  ~~~
  这时候可以查看一下是否配置到位：
  ![image](https://github.com/light2001/MyDocs/assets/3821091/edeb1270-fdb0-44ae-8c82-d74921d0fa6f)

- 设置推送账号
  ~~~
  git config --global credential.https://github.com.username <your_username>
  ~~~

  参考：https://www.baeldung.com/ops/git-configure-credentials

  - 查看.git-credential
    ![image](https://github.com/light2001/MyDocs/assets/3821091/aafa77e7-1eee-47c2-bdd4-0b590eb73629)
    可以看到有好不同的记录
