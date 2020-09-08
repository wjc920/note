1. [下载离线包](https://download.docker.com/linux/ubuntu/dists/xenial/pool/stable/amd64/)

离线安装docker需要下载3个包，containerd.io ，docker-ce-cli，docker-ce

2. 下载完毕后拷贝到ubuntu上用 dpkg 命令安装，先安装 containerd.io 跟 docker-ce-cli，最后安装docker-ce，命令

sudo dpkg -i xxxx.deb