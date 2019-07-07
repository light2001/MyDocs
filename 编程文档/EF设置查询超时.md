#### EntityFramework 如何配置Sql查询超时问题

  只需要在DBContext中加上这句话就好了

  ```

     public MyInfoDbContext(DbContextOptions<MyInfoDbContext> options)
            : base(options)
        {
            this.Database.SetCommandTimeout(600000);
        }


  ```