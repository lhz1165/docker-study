# WIN10/11 安装WSL2

### 环境要求

必须运行 Windows 10 版本 2004 及更高版本,win+r winver

#### 步骤1.启用虚拟机平台和 Linux 子系统功能

方式一:控制面板

方式二：powershell开启

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

#### 步骤2.设置wsl默认版本为Wsl2

```
wsl --set-default-version 2
```

#### 步骤3.安装一个Linux发行版

直接去微软商店下载,然后升级到2

```
wsl -l -v
wsl --set-version Ubuntu-20.04 2
```

#### 常用命令

查看已安装的Linux发行版

```
wsl -l --all -v
```

卸载当前Linux发行版

```
wsl --unregister Ubuntu-20.04
```

转移位置

```
导出Linux发行版tar文件到D盘
wsl --export Ubuntu-20.04 d:/wsl-ubuntu-20.04.tar

重新导入并安装WSL2到D盘
wsl --import Ubuntu-20.04 d:/wsl-ubuntu-20.04 d:/wsl-ubuntu-20.04.tar --version 2
设置默认登录用户为安装时用户名
ubuntu2004 config --default-user USERNAME
```

列出可用的 Linux 发行版

```
wsl --list --online
```

设置默认 WSL 版本

```
wsl --set-default-version <Version>
```

设置默认 Linux 发行版

```
wsl --set-default <Distribution Name>
```

检查 WSL 状态

```
wsl --status

```

