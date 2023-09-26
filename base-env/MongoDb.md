# MongoDb

```
 docker pull mongo:4.4


mkdir -p /docker_volume/mongodb/data


docker run -itd --name mongo -v /docker_volume/mongodb/data:/data/db -p 27017:27017 mongo:4.4 (--auth)
–auth：需要密码才能访问容器服务


docker exec -it mongo mongo admin
db.createUser({ user:'root',pwd:'123456',roles:[ { role:'userAdminAnyDatabase', db: 'admin'},'readWriteAnyDatabase']});


```

