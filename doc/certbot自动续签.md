certbot自动续签

```shell
apt update -y && apt install -y certbot
```

##### 确认80和443未被占用

##### 停止nginx

```shell
curl -s ipv4.ip.sb  #查看ip
```

##### 申请证书

```shell
certbot certonly --standalone -d $yuming --email your@email.com --agree-tos --no-eff-email --force-renewal
```

$yuming  为域名的地址

##### **证书存放目录**

ls /etc/letsencrypt/live/

**自动续签脚本**

```shell
curl -O https://raw.githubusercontent.com/kejilion/sh/main/auto_cert_renewal-1.sh

chmod +x auto_cert_renewal-1.sh

./auto_cert_renewal-1.sh
```

**定时执行**

```shell
echo "0 0 * * * cd ~ && ./auto_cert_renewal-1.sh" | crontab -

crontab -e
```



