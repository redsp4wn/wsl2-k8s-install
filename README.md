# wsl2-k8s-install
在windows环境下使用wsl2搭建k8s环境

# 先决条件
必须运行 Windows 10 版本 2004 及更高版本（内部版本 19041 及更高版本）或 Windows 11 才能使用以下命令。 如果使用的是更早的版本，请参阅[链接](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual)。

# 安装 WSL 命令
在管理员模式下打开 PowerShell 或 Windows 命令提示符，方法是右键单击并选择“以管理员身份运行”，输入 wsl --install 命令，然后重启计算机。
```powershell
wsl --install
```
此命令将启用运行 WSL 并安装 Linux 的 Ubuntu 发行版所需的功能。 （可以更改此默认发行版）。

# 安装 Docker Desktop
1、下载 [Docker Desktop](https://docs.docker.com/docker-for-windows/wsl/#download) 并按照安装说明进行操作。
2、确保在“设置”>“常规”中选中“使用基于 WSL 2 的引擎”。
![设置1](https://learn.microsoft.com/zh-cn/windows/wsl/media/docker-running.png "Magic Gardens")
3、通过转到“设置”>“资源”>“WSL 集成”，从要启用 Docker 集成的已安装 WSL 2 发行版中进行选择。
![设置2](https://learn.microsoft.com/zh-cn/windows/wsl/media/docker-dashboard.png "Magic Gardens")

# 安装 Kubernetes
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

aaa