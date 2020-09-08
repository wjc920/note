# Docker安装

Docker安装好之后，使用`sudo service docker start`仍然无法启动docker-deamon，主要原因是没有权限，需要以管理员的方式启动WSL，如果仍然无效，可能需要重启电脑（再不行需要安装并执行sudo cgroupfs-mount）