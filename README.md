# 甲骨文实例抢购教程

## 获取程序
- 如果需要在本地电脑运行该程序，根据自己电脑的CPU架构类型，打开下面的 `下载地址` 下载对应的文件即可。如果需要在服务器上运行该程序，那么根据服务器的CPU架构类型选择对应的文件下载到服务器即可。

- 下载完成后解压压缩包，可以得到可执行程序 (Windows系统: `oci-help.exe` , 其他操作系统: `oci-help` ) 和 配置文件 `oci-help.ini` 。

> 下载地址: https://github.com/lemoex/oci-help/releases/latest


## 获取配置信息
![image](https://github.com/lemoex/oci-help/raw/main/doc/1.png)
![image](https://github.com/lemoex/oci-help/raw/main/doc/2.png)
![image](https://github.com/lemoex/oci-help/raw/main/doc/3.png)
![image](https://github.com/lemoex/oci-help/raw/main/doc/4.png)
![image](https://github.com/lemoex/oci-help/raw/main/doc/5.png)
![image](https://github.com/lemoex/oci-help/raw/main/doc/6.png)


## 编辑配置文件
用文本编辑器打开在第一步获取到的 `oci-help.ini` 文件，进行如下配置:

![image](https://github.com/lemoex/oci-help/raw/main/doc/7.png)
![image](https://github.com/lemoex/oci-help/raw/main/doc/8.png)

## Telegram 消息提醒配置
![image](https://github.com/lemoex/oci-help/raw/main/doc/9.png)

> BotFather: https://t.me/BotFather    
> IDBot: https://t.me/myidbot


## 运行程序
程序运行支持以下参数:
- `-config` 或 `-c`: 指定配置文件的路径，默认为 `./oci-help.ini`。
- `-action`: 指定要执行的操作，可选值包括:
  - `launch-all`: 批量创建实例。
  - `list-ips-all`: 批量导出所有实例的公共IP。

### go build 打包命令

```bash
# 在当前操作系统下打包
go build -o oci-help main.go

# 在 Windows PowerShell 命令行打包linux执行文件
$env:GOOS="linux"; $env:GOARCH="amd64"; go build -o oci-help main.go

```

### 直接运行
```bash
# 前台运行程序
./oci-help

# 运行指定操作 (例如: 批量创建实例)
./oci-help -action launch-all

# 运行指定操作并指定配置文件
./oci-help -action launch-all -config /path/to/your/oci-help.ini

# 前台运行需要一直开着终端窗口，可以在 Screen 中运行程序，以实现断开终端窗口后一直运行。
# 创建 Screen 终端
screen -S oci-help 
# 在 Screen 中运行程序
./oci-help
# 离开 Screen 终端
按下 Ctrl 键不松，依次按字母 A 键和 D 键。或者直接关闭终端窗口也可以。
# 查看已创建的 Screen 终端
screen -ls
# 重新连接 Screen 终端
screen -r oci-help
```

### Docker 运行
```bash
# Dockerfile文件放到服务器上的任意目录下

# 在目录下执行命令 构建 Docker 镜像
docker build -t oci-help .

# 运行 Docker 容器 (前台运行)，/path/to/your/oci-help-directory 为存放oci-help执行文件、oci-help.ini和密钥等文件的目录
docker run --name oci-help --restart unless-stopped -v /path/to/your/oci-help-directory:/app oci-help

# 后台运行 Docker 容器并指定操作 (例如: 批量创建实例)，/path/to/your/oci-help-directory 为存放oci-help执行文件、oci-help.ini和密钥等文件的目录
docker run -d --name oci-help --restart unless-stopped -v /path/to/your/oci-help-directory:/app oci-help -action launch-all

# 查看 Docker 容器日志
docker logs oci-help

# 停止并删除 Docker 容器
docker stop oci-help
docker rm oci-help
```