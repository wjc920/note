# Docker安装

## Ubuntu

1. [下载离线包](https://download.docker.com/linux/ubuntu/dists/xenial/pool/stable/amd64/)

    离线安装docker需要下载3个包，containerd.io ，docker-ce-cli，docker-ce

2. 下载完毕后拷贝到ubuntu上用 dpkg 命令安装，先安装 containerd.io 跟 docker-ce-cli，最后安装docker-ce，命令
    ```
    sudo dpkg -i xxxx.deb
    sudo service docker start
    ```
   Centos安装
   ```
   rpm -ivh *.rpm
   systemctl enable docker
   service docker start
   ```
3. 配置网易镜像库
    ```
    # vi /etc/docker/daemon.json
    {
        "registry-mirrors": ["http://hub-mirror.c.163.com"]
    }
    ```



## Centos

1. [下载离线包](https://download.docker.com/linux/centos/7/x86_64/stable/Packages/)

    离线安装docker需要下载4个包，containerd.io ，docker-ce-cli，docker-ce，docker-ce-rootless-extras

2. 安装rpm
   ```
   rpm -ivh *.rpm
   systemctl enable docker
   service docker start
   ```
3. 配置网易镜像库
    ```
    # vi /etc/docker/daemon.json
    {
        "registry-mirrors": ["http://hub-mirror.c.163.com"]
    }
    ```


# Docker Compose安装(离线安装)

```
su root
cp docker-compose-Linux-x86_64 /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

> [Docker Compose安装包下载](https://github.com/docker/compose/releases)