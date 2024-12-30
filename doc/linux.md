---
outline: deep
---

# linux

安装deb软件

```js
dpkg -i 包名
```

查看所有通过pdkg安装的软件

```js
dpkg -l 
```

需要安装这个依赖  用于查询依赖

```js
apt-file search  包名 
```

用来查询包的在linux中安装在什么位置

```js
whereis  包名
```

修改包的权限

```js
sudo chmod 777 electron-vue3
```

查询库所在包插件

```js
sudo apt-get install apt-file
```

更新apt-file的缓存

```js
apt-file update
```

###### 查找所在的包

```js
apt-file search libz.so.1
```

重启服务系统

```js
reboot
```

移动文件或者重命名

```js
mv 文件 ..
mv 文件1 文件2
```

如果出现vim警告或者报错 daemon.json报错

```bash	
sudo rm /etc/docker/.daemon.json.swp
```



##### vim快捷键

ggVG 全选

```bash
gg 将光标移动到文件顶部
V 进入行选择模式
G 将光标移动到底部
y 复制
d 剪切
p 粘贴
u 撤销
ctrl+r 反撤销
删除 dw
```



## nginx

启动

```js
nginx
```

停止

```js
nginx -s stop 
```



###### 重新加载配置文件

```js
nginx -s reload 
```

检查配置文件

```js
nginx -t
```



## ufw防火墙

关闭防火墙

```js
sudo ufw disable 
```



