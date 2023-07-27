# Tomcat





```
docker pull tomcat:8

docker run -p 8080:8080  -v /home/lhz/tomcatdata/webapps:/usr/local/tomcat/webapps --name tomcat --link mysql8:mysql8 -e TZ=Asia/Shanghai -d tomcat:8
```





进入tomcat目录

把  webapps.dist 移到 webapps 

rm -rf webapps

rm webapps.dist webapps



 docker  inspect  mysql8 找到ipaddress

修改数据库配置mysql为docker的ip





端口号后面一定要加上目录名称

http://localhost:8080/LR_Project_war/login.jsp/







