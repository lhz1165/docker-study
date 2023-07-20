# Maven

如果项目太大，打包父工程时间太多，但是单独打包又包含以来，可以使用命令指定打包某些模块

```shell
-pl 打包指定模块，以逗号分隔
-am 打包所指定模块的依赖模块

//1 指定依赖和要运行的模块
mvn clean package -pl lyt-viid-common,lyt-viid-mapper,./lyt-viid-other/lyt-viid-openinvoke

//2 指定运行的模块，-am 自动寻找依赖
mvn clean package -pl ./lyt-viid-other/lyt-viid-openinvoke -am
```

