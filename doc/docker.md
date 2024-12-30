# docker

## 添加国内镜像源

创建daemon.json文件，并添加镜像地址sudo vim /etc/docker/daemon.json

```bash	
{
  "registry-mirrors": [
        "https://hub.rat.dev",
        "https://docker.m.daocloud.io",
        "https://docker.chenby.cn",
        "https://dhub.kubesre.xyz"
    ]
}
```

重启Docker

```bash	
sudo service docker restart
systemctl restart docker
```

查看添加的国内源是否生效

```bash	
sudo docker info | grep Mirrors -A 4
```

结果

```bash
 Registry Mirrors:
  https://registry.docker-cn.com/
  http://hub-mirror.c.163.com/
  https://docker.mirrors.ustc.edu.cn/
  https://kfwkfulq.mirror.aliyuncs.com/
WARNING: No cpu cfs quota support
WARNING: No cpu cfs period support
WARNING: No cpu shares support
WARNING: No cpuset support
WARNING: No io.weight support
WARNING: No io.weight (per device) support
WARNING: No io.max (rbps) support
WARNING: No io.max (wbps) support
WARNING: No io.max (riops) support
WARNING: No io.max (wiops) support
WARNING: bridge-nf-call-iptables is disabled
WARNING: bridge-nf-call-ip6tables is disabled
```

可以看到，刚添加的4个国内镜像源已经生效。

检查配置文件

```bash
docker info
```

查看所有的容器

```bash
docker ps -a
docker stop  #停止容器
docker rm name #删除容器
docker rmi name  #停止并删除容器
```



## docker安装jenkins

安装

```js
docker pull jenkins/jenkins
```

启动服务挂到8083

```bash
docker run -d -uroot -p 9095:8080 -p 50000:50000 --name jenkins -v /home/jenkins_home:/var/jenkins_home -v /etc/localtime:/etc/localtime jenkins/jenkins
-d #表示后台运行不占用终端
-p 8083:8080  #这是端口映射的设置，表示将宿主机的 8083 端口映射到容器内的 8080 端口。Jenkins 默认使用 8080 端口，所以这意味着你可以通过访问宿主机的 8083 端口来访问 Jenkins
--name jenkins #给启动的容器命名为 jenkins
-v /usr/local/jenkins/jenkins_home:/home/jenkins_home #这是一个卷（volume）挂载设置，将宿主机的目录 /usr/local/jenkins/jenkins_home 挂载到容器内的 /home/jenkins_home 目录。这样做的目的是将 Jenkins 的数据（例如配置、插件、构建记录等）保存在宿主机上，即使容器重启或删除，数据也会持久保存
jenkins/jenkins:2.344 #这是要使用的 Docker 镜像和标签。jenkins/jenkins 是 Jenkins 官方提供的 Docker 镜像，:2.344 是镜像的标签，表示使用 Jenkins 的 2.344 版本。
```

开启服务器的8083端口

获取初始化的密码

```bash
docker exec -it jenkins bash #进入容器内
cat /var/jenkins_home/secrets/initialAdminPassword
```

此时就成功了





## gitlab搭建

##### 查询可用docker镜像

```bash
docker search gitlab
```

##### 下载镜像

```bash
docker pull gitlab/gitlab-ce
```

##### 启动服务

```bash
docker run -d -p 10008:80 -p 10009:443 -p 10010:22 --restart always --name gitlab -v /docker/gitlab/etc/gitlab:/etc/gitlab -v /docker/gitlab/var/log/gitlab:/var/log/gitlab -v /docker/gitlab/var/opt/gitlab:/var/opt/gitlab --privileged=true gitlab/gitlab-ce
```

##### 修改gitlab.rb文件

```bash	
vi /docker/gitlab/etc/gitlab/gitlab.rb
```

修改如下位置

```bash	
# 如果使用公有云且配置了域名了，可以直接设置为域名，如下
external_url 'http://gitlab.redrose2100.com'
# 如果没有域名，则直接使用宿主机的ip，如下
external_url 'http://172.22.27.162'  

# 同样如果有域名，这里也可以直接使用域名
gitlab_rails['gitlab_ssh_host'] =  'gitlab.redrosee2100.com'
# 同样如果没有域名，则直接使用宿主机的ip地址
gitlab_rails['gitlab_ssh_host'] = '172.22.27.162'
```

```bash	
# 端口为启动docker时映射的ssh端口
gitlab_rails['gitlab_shell_ssh_port'] =10010 
```

##### 关于邮箱发邮件的配置如下

```bash	
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "smtp.163.com"   # 邮箱服务器
gitlab_rails['smtp_port'] = 465    # 邮箱服务对应的端口号
gitlab_rails['smtp_user_name'] = "hitredrose@163.com"   # 发件箱的邮箱地址
gitlab_rails['smtp_password'] = "xxxxxxxxxxx"      # 发件箱对应的授权码，注意不是登录密码，是授权码
gitlab_rails['smtp_domain'] = "163.com"
gitlab_rails['smtp_authentication'] = "login"
gitlab_rails['smtp_enable_starttls_auto'] = true
gitlab_rails['smtp_tls'] = true
gitlab_rails['gitlab_email_enabled'] = true
gitlab_rails['gitlab_email_from'] = 'hitredrose@163.com'     # 发件箱地址
gitlab_rails['gitlab_email_display_name'] = 'gitlab.redrose2100.com'    # 显示名称
gitlab_rails['gitlab_email_reply_to'] = 'noreply@example.com'     # 提示不要回复
```

##### 重启docker

```bash	
docker restart gitlab
进入docker容器里
docker exec -it gitlab bash

vi /opt/gitlab/embedded/service/gitlab-rails/config/gitlab.yml

gitlab:
##Web server settings (note:host is the FQDN,do not include http://)
host:
port:
https: false

#重启gitlab
gitlab-ctl restart
```

查看root默认密码

```bash	
cat /docker/gitlab/etc/gitlab/initial_root_password
```

