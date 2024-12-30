# windows

## window10

#### 删不掉的文件夹

创建一个txt文件里面写

```
DEL /F /A /Q \\?\%1
RD /S /Q \\?\%1
```

保存后修改名称为Delete.bat

```text
然后把要删除的文件夹拖到“Delete.bat”这个文件上，即可直接删除了。
```