# 镜像
### 镜像列表
```shell
docker images
```
**--digests=true|false**：为true时，镜像列表多显示一列，如下：
|DIGEST|
|--|
|sha256:9183655bb75a7fdeaec96d5f84a56d4363c672d596f4ae25e01e957529d97f4e|

### tag

```shell
# 在centos-7.7.1908:20200424镜像上新增tag wjc-centos:latest
docker tag centos-7.7.1908:20200424 wjc-centos:latest
```

### 镜像详细信息

```shell
docker inspect wjc-centos:latest
```
得到的镜像详细信息是JSON格式的，如果想让信息精简一些可以使用`-f {{".RootFS.Layers"}}`，来获取详细信息中的某一个子条目。

### 查看创建历史
```shell
docker history wjc-centos
```
**--no-trunc**：查看完整信息

### 删除和清理镜像
```shell
# 根据镜像tag删除
docker rmi wc1:latest
# 根据镜像ID删除
docker rmi 6dbf8162bf50 -f
# 删除所有临时文件，加-a的话可以在删除临时文件的同时删除所有无用镜像
docker image prune
```
- 根据tag删除，只会删除对应tag，只有当镜像只剩下一个tag时，删除tag才会删除竟像文件；
- 根据ID删除镜像，直接会删除ID相同的所有tag和镜像文件
- 删除镜像必须先删除镜像对应容器（建议，可以加-f来强行删除）

### 创建镜像
- 基于已有容器创建
```shell
# 启动交互式容器
docker run -it 718aa89713c8 bash
# 修改镜像
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
# 创建镜像 a：作者；m：提交说明
docker commit -m "tz update" -a "wjc" 26969b394f5c centos:0426
```
- 直接导入
```shell
# 保存镜像到本地
docker save -o centos.tar centos:0426
# 导入镜像
docker load -i centos.tar
# 保存容器到本地
docker export -o container.tar containerId 
# 导入镜像
docker import centos.tar centos:import
```
后面两种导入导出一般针对容器。前两种针对镜像，前两种方法能保存镜像的创建和更新历史信息。
- [Dockerfile创建](Dockerfile指南.md)

# 容器

### 日志
```shell
# 查看容器日志
docker logs --since 2020-04-16T11:28:00 --until 2020-04-16T11:28:59 45c5c192a01c > /tmp/tmp
```
![]()
