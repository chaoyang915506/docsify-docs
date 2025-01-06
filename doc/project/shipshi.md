# 砂石项目

###### 打包命令行

```js
run.exe  --encoder vitl   --pred-only --grayscale --img-path D:\Ffile\dinasShip\ship_server\public\img2
 --outdir D:\Ffile\dinasShip\ship_server\public\img2
```

运行

```js
python run.py   --encoder vitl   --pred-only --grayscale --img-path D:\Ffile\dinasShip\ship_server\public\img2 --outdir D:\Ffile\dinasShip\ship_server\public\img2
```



###### 去除打包console

```js
pyinstaller -D --noconsole run.py 
```



