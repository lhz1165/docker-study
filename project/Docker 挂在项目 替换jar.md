# Docker 挂在项目 替换jar

编写Dockerfile

```dockerfile
# 该镜像需要依赖的基础镜像
FROM openjdk:8-jre-slim
#时区设置
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN mkdir /target/
# 将当前目录下的jar包复制到docker容器的/目录下  改成自己项目的名字
# ADD target/myproject-*.jar /target/myproject-0.0.1-SNAPSHOT.jar
# 容器暴露13333和5005端口
EXPOSE 13333
EXPOSE 5005
# 指定docker容器启动时运行jar包  同时开启5005用来idea远程debug
ENTRYPOINT ["java", "-jar","-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005","/target/myproject-0.0.1-SNAPSHOT.jar"]

# 指定维护者的名字
MAINTAINER lhz
```

构建镜像 myproject:0.1为镜像名

```
docker build -t myproject:0.1 .
```



启动镜像并挂载本地目录（windows系统中/启动时在Desktop可视化页面启动）

```
docker run --name myproject-cointer -d -p 13333:13333 -p 5005:5005 --privileged=true -v D:\java\PROJECT_SPASE\myproject\target:/target myproject:0.1
```



之后每次去docker /target看看，就可以发现是自己本地项目的target文件夹，

maven打包好了只需要重启容器，就可以执行新的代码

```
mvn clean package -pl myproject -am
```



pub-system 打包

```
//ubuntu里面
//pub image
docker build -t pub:v1 .
//pub container
docker run --name pub-system -d -p 12006:12006 -v /mnt/d/java/PROJECT_SPASE/public-/pub-system/buss/target:/target pub:v1
```

