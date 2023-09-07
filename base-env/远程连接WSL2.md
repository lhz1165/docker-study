# 远程连接WSL2



```shell
sudo apt-get remove --purge openssh-server   ## 先删ssh
sudo apt-get install openssh-server          ## 在安装ssh  
sudo rm /etc/ssh/ssh_config                  ## 删配置文件，让ssh服务自己想办法链接
sudo service ssh --full-restart

sudo vim /etc/ssh/sshd_config
Port 6666
ListenAddress 0.0.0.0
PasswordAuthentication yes

## 每次重启wsl都要执行该语句
sudo service ssh --full-restart

## 重新生成host key
sudo dpkg-reconfigure openssh-serve
```

