# 必装软件

GNOME Tweaks

# 系统显卡设置

等系统进入grub后，按esc，选高级，进recover，先network再resume，设置显卡驱动,具体设置位置在 软件和更新->附加驱动,选择NVIDIA版本。字体

字体位置在/usr/share/fonts,将Windows字体文件copy到该文件夹下,并执行如下脚本

```shell
cd /usr/share/fonts/winFontsDir //进入创建的字体目录 
sudo chmod 744 * 
sudo mkfontscale 
sudo mkfontdir 
sudo fc-cache -f -v 
```

# 交换区

ubuntu18.04默认的swap文件在根目录/下，名字是swapfile

1.查看交换分区大小

free -m 

在创建完毕后也可以用这个命令查看内存情况

2.创建一个swap文件
sudo dd if=/dev/zero of=swap bs=1024 count=8000000

创建的交换文件名是swap，后面的80000000是8g的意思，可以按照自己的需要更改

3.创建swap文件系统
sudo mkswap -f swap

4.开启swap
sudo swapon swap

5.关闭和删除原来的swapfile
sudo swapoff  swapfile

sudo rm /swapfile

6.设置开机启动
sudo vim /etc/fstab

将里面的swapfile改为swap

# 触控板左右键失灵

```shell
gsettings set org.gnome.desktop.peripherals.touchpad click-method areas
```



