# frp使用

#### 下载对应的frp版本

https://github.com/fatedier/frp/tags

下载

wget https://github.com/fatedier/frp/releases/download/vX.X.X/frp-X.X.X-linux-amd64.tar.gz 

tar -zxvf frp-X.X.X-linux-amd64.tar.gz

##### 服务端配置 frps.toml

```bash
bindPort = 7000
# 默认为 127.0.0.1，如果需要公网访问，需要修改为 0.0.0.0。
webServer.addr = "0.0.0.0"
webServer.port = 7500
# dashboard 用户名密码，可选，默认为空
webServer.user = "admin"
webServer.password = "admin"

vhostHTTPPort = 8001
```

##### 客户端配置frpc.toml

```bash
serverAddr = "公网ip"
serverPort = 7000 #对外暴露的端口 需要打开防火墙的配置

[[proxies]]
name = "ssh1"  
type = "tcp"
localIP = "127.0.0.1"
localPort = 22
remotePort = 6000
#可以通过ssh进行连接

[[proxies]]
name = "web01"
type = "tcp"
localIP = "127.0.0.1"
localPort = 10081 #本地的端口
remotePort = 10081 #本地的端口 防火墙也需要开启不然访问会被拦截
```

##### 安装ststemd

```bash
# 使用 yum 安装 systemd（CentOS/RHEL）
yum install systemd

# 使用 apt 安装 systemd（Debian/Ubuntu）
apt install systemd

```

**创建 frps.service 文件**

使用文本编辑器 (如 vim) 在 `/etc/systemd/system` 目录下创建一个 `frps.service` 文件，用于配置 frps 服务。

```bash
$ sudo vim /etc/systemd/system/frps.service
也可以直接去文件夹直接touch 创建frps.service
```

写入内容

```bash
[Unit]
# 服务名称，可自定义
Description = frp server
After = network.target syslog.target
Wants = network.target

[Service]
Type = simple
# 启动frps的命令，需修改为您的frps的安装路径
ExecStart = /path/to/frps -c /path/to/frps.toml

[Install]
WantedBy = multi-user.target
```

**使用 systemd 命令管理 frps 服务**

```bash	
# 启动frp
sudo systemctl start frps
# 停止frp
sudo systemctl stop frps
# 重启frp
sudo systemctl restart frps
# 查看frp状态
sudo systemctl status frps
# 更新配置文件
systemctl status frps

```

**设置 frps 开机自启动**

```bash	
sudo systemctl enable frps
```

