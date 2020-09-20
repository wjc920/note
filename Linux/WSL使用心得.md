# Docker安装

Docker安装好之后，使用`sudo service docker start`仍然无法启动docker-deamon，主要原因是没有权限，需要以管理员的方式启动WSL，如果仍然无效，可能需要重启电脑（可能不需要使用管理员权限运行也行，只需要在docker安装好之后重启电脑即可）

# WSL迁移

## 更换WSL安装目录

```
LxRunOffline l
LxRunOffline m -n Ubuntu-18.04 -d C:\Users\WJC\WSL
LxRunOffline di -n Ubuntu-18.04
```

## 不同系统之间迁移

```
# 最好导出的目录和导入时的目录路径相同，例如，导出到D盘根目录时，导入时也放在D盘根目录
LxRunOffline e -n <WSL名称> -f <压缩包路径>.tar.gz
LxRunOffline i -n <WSL名称> -d <安装路径> -f <压缩包路径>.tar.gz
```