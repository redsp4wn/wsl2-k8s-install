# wsl2-k8s-install
在windows环境下使用wsl2搭建k8s环境

## 先决条件
必须运行 Windows 10 版本 2004 及更高版本（内部版本 19041 及更高版本）或 Windows 11 才能使用以下命令。 如果使用的是更早的版本，请参阅[链接](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual)。

## 安装 WSL 命令
在管理员模式下打开 PowerShell 或 Windows 命令提示符，方法是右键单击并选择“以管理员身份运行”，输入 wsl --install 命令，然后重启计算机。
```powershell
wsl --install
```
此命令将启用运行 WSL 并安装 Linux 的 Ubuntu 发行版所需的功能。 （可以更改此默认发行版）。

## 安装 Docker Desktop
1、下载 [Docker Desktop](https://docs.docker.com/docker-for-windows/wsl/#download) 并按照安装说明进行操作。

2、确保在“设置”>“常规”中选中“使用基于 WSL 2 的引擎”。
![设置1](https://learn.microsoft.com/zh-cn/windows/wsl/media/docker-running.png "Magic Gardens")

3、通过转到“设置”>“资源”>“WSL 集成”，从要启用 Docker 集成的已安装 WSL 2 发行版中进行选择。
![设置2](https://learn.microsoft.com/zh-cn/windows/wsl/media/docker-dashboard.png "Magic Gardens")

4、设置docker镜像加速，修改设置中的Docker Engine配置文件，将镜像加速器地址添加到配置文件中。
```json
{//实例镜像地址不一定生效，建议使用阿里云镜像加速器地址
  "registry-mirrors": [
    "https://docker.mirrors.ustc.edu.cn",
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com"
  ]
}
```
![设置3](Screenshots\docker-mirrors.png "Magic Gardens")

## 安装 Kubernetes
1、下载kind二进制文件
```
wsl curl -Lo /usr/bin/kind https://kind.sigs.k8s.io/dl/v0.10.0/kind-linux-amd64

chmod +x /usr/bin/kind

kind version
```
2、在 PowerShell 中运行以下命令以创建一个名为 kind 的集群
```powershell
wsl kind create cluster
```
3、删除集群
```powershell

wsl kind delete cluster
```

## 注意事项
### 系统迁移
wsl子系统默认安装在C盘，如果C盘空间不足，可以通过以下命令将wsl子系统安装在其他盘符
```powershell
#关闭所有子系统
wsl --shutdown
#导出子系统Ubuntu到E:\wsl2\ubuntu.tar
wsl --export Ubuntu E:\wsl2\ubuntu.tar
#删除子系统Ubuntu
wsl --unregister Ubuntu
#从E:\wsl2\ubuntu.tar导入子系统Ubuntu
wsl --import Ubuntu E:\wsl2\ubuntu E:\wsl2\ubuntu.tar --version 2
```

