# 常见问题
- 下载或者卸载APP时，显示依赖错误
```shell
# 执行脚本即可
sudo apt-get dist-upgrade
```
- 文件压缩和解压缩
```shell
tar -czvf test.tar.gz a.c
tar -tzvf test.tar.gz
tar -xzvf test.tar.gz -C /tmp/
```
# 权限
## 文件或者目录权限修改
```shell
# -R 递归执行子目录权限修改
chmod -R 777 /home/user
```