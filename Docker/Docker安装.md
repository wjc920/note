# Docker安装

1. [下载离线包](https://download.docker.com/linux/ubuntu/dists/xenial/pool/stable/amd64/)

    离线安装docker需要下载3个包，containerd.io ，docker-ce-cli，docker-ce

2. 下载完毕后拷贝到ubuntu上用 dpkg 命令安装，先安装 containerd.io 跟 docker-ce-cli，最后安装docker-ce，命令
    ```
    sudo dpkg -i xxxx.deb
    sudo service docker start
    ```
3. 配置网易镜像库
    ```
{
  "registry-mirrors": ["http://hub-mirror.c.163.com"]
}
    ```

# Docker Compose安装
```
# 在线下载，比较慢
# sudo curl -L "https://github.com/docker/compose/releases/download/1.27.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
# 离线下载后安装
sudo cp docker-compose-Linux-x86_64 /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```