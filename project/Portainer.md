# Portainer

起步

```
docker pull portainer/portainer-ce

docker run -d -p 9000:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --name portainer portainer/portainer-ce
```

