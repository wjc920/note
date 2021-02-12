# 环境变量配置

```
export JAVA_HOME=/root/cluster/jdk1.8.0_261
export PATH=$PATH:$JAVA_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```

> 建议在 `/etc/profile.d/` 目录下新建一个类似 `env.sh` 的脚本，将上面几行代码放进去，之后再执行 `source /etc/profile`
