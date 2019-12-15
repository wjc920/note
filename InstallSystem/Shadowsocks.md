1. 添加源

```shell
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
```

> Ubuntu18, sudo apt-get update在执行的时候可能会报如下错误:
>
> ```
> 错误:5 http://ppa.launchpad.net/hzwhuang/ss-qt5/ubuntu bionic Release                     
>   404  Not Found [IP: 91.189.95.83 80]
> ```
>
> 处理办法:
>
> ```shell
> cd /etc/apt/sources.list.d/
> sudo vim hzwhuang-ubuntu-ss-qt5-bionic.list
> ```
>
> 将bionic修改为xenial

2. 安装ss

```shell
sudo apt-get install shadowsocks-qt5
```

3. 配置

   配置文件在`网盘/ComputerInstall/shadowsocks`

4. Chrome代理配置

   4.1 搜索程序, 设置->网络->网络代理->手动->socks, 127.0.0.1:1080,开启系统网络代理

   4.2 登录Chrome账户,开启同步

   4.3 `网盘/ComputerInstall/shadowsocks`下将SwitchyOmega的配置文件下载,再将配置导入

   4.4 回到`4.1`禁用代理