---
outline: deep
---

# pm2
自启动方案

[csdn参考实现](https://blog.csdn.net/qq_41579327/article/details/128109002?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522171947041416800225576786%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=171947041416800225576786&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-128109002-null-null.142^v100^pc_search_result_base2&utm_term=pm2%20%E5%A6%82%E4%BD%95%E5%AE%9E%E7%8E%B0%E5%9C%A8window%E4%B8%8A%E8%87%AA%E5%90%AF%E5%8A%A8&spm=1018.2226.3001.4187)

## 安装

```js
npm i -g pm2-windows-service
```

管理员运行

```js
pm2-service-install   
```

Perform environment setup ?  选 n , 回车

通过win+r,输入`services.msc`查看PM2服务已安装并已启动

```js
services.msc
```

安装pm2到全局

```js
npm install pm2 -g
```

安装windows自启动包

```js
npm install pm2-windows-startup -g
```

安装服务 pm2-service-install -n myservice （安装后在windows服务中多了一个myservice的服务）

```js
npm i pm2-windows-service -g
```

创建开机启动脚本文件

```js
pm2-startup install
```

使用pm2启用项目(实现自启)

```js
pm2 start 路径 --name 名称
```

保存pm2中的项目

```js
pm2 save
```

重启电脑可以查看（ 以表格显示)

```js
pm2 ls
```

如果要卸载服务，执行

```js
pm2-service-uninstall
```

启动一个服务，携带 --name 参数添加一个应用名，携带参数 --watch 将观察修改重启服务

```js
pm2 start     
```

列出当前的服务

```js
pm2 list 
```

监视每个node进程的CPU和内存的使用情况

```js
pm2 monit  
```

停止服务(pm2 stop 名称或id)

```js
pm2 stop 0  
```

```js
//停止所有服务进程
pm2 stop all   
//重启服务(pm2 restart app.js)
pm2 restart 0  
//重启所有进程
pm2 restart all 
//删除服务(pm2 delete app_name|app_id)
pm2 delete 0    
//删除全部服务
pm2 delete all  
// 查看所有服务的输出日志
pm2 logs        
//查看服务的输出日志
pm2 logs 0      
```

