#### SpringBoot在Docker下部署注意事项
- DockerCompose如何编写

  使用DockerCompose编写部署文件的时候，必须加上network_mode: "host" 这句话，否则会部署失败
  这给出我目前使用的DockerCompose.yml

  ```
  version: '3.1'

  services:

      Cex_Server:
          image: cex
          build:
              context: ../src/target/
          ports:
              - "9002:80"
          network_mode: "host"
          expose:
              - "9002"

  ```

- JDK镜像的选择

  JDK镜像如果你通过Docker search搜索出来会看到无数结果，我们只使用以下镜像

  java:8

- Dockerfile编写，以下给出我目前使用的

```
  FROM java:8

  WORKDIR /home
  COPY CEX_Api-1.0.11.jar app.jar

  ENTRYPOINT ["java","-jar","app.jar"]

```