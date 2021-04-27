# 初始环境配置


**步骤1：** `/etc/bash.bashrc`

```shell
TERM="cygwin"
source /etc/profile.d/lang.sh
alias ll='ls -l'
alias ls='ls -F --color=auto --show-control-chars'
PS1="\[\e]0;\w\a\]\[\e[35;1m\][\u@\h \W]# \[\e[0m\]"

HOME="/cygdrive/c/Users/$USERNAME"
HISTFILE="/cygdrive/d/Cache/.bash_history"
HISTFILESIZE=1000
```

- 

# 常见问题

## 1 Cygwin bash终端很难用

默认情况下，bash使用的是Windows自带的终端，所以很难用。不过这个终端有一个好处，可以集成到IDEA中去。如果想完全体验linux下的终端，可以选择mintty终端（该终端不能集成到IDEA中）。

## 2 PS1提示符设置

可配置到环境变量或者添加到`~/.bashrc`

> 可根据关键词`shell PS1`在搜索引擎上搜索

```
# 粉红色
PS1="\[\e[35;1m\][\u@\h \W]# \[\e[0m\]"
```

## 使用Cygwin后导致Maven日志乱码

添加如下环境变量即可

```shell
export TERM="cygwin"
```
