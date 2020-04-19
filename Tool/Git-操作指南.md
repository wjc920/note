# git使用前配置

### 查看

```shell
#查看当前用户名
git config user.name
#查看当前用户邮箱
git config user.email
```

### 修改

```shell
#配置全局用户名WJC
git config --global user.name "wjc"
#配置全局用户邮箱wjc920@126.com
git config --global user.email "wjc920@foxmail.com"
#设置中文编码
git config --global core.quotepath false
#执行下面语句生成密钥，并添加密钥到server
ssh-keygen -t rsa -C "wjc920@foxmail.com" 
#复制id_rsa.pub到git server
```

# 初始化本地仓库并推送到远程库

```shell
git init #初始化本地仓库
在远程库上新建仓库
git remote add origin https://git.oschina.net/xxx/.git(或则 git:git的地址) #关联本地仓库到远程仓库

git add * #添加要提交的文件到暂存区
git commit -m "init commint" #提交代码到文件控制仓库
git fetch origin #将远程主机的更新，全部取回本地 
git pull origin master --allow-unrelated-histories #拉
git push -u origin master #取远程分支代码到本地
```

# 远程库连接

```shell
git clone https://github.com/JustLikeY/scrum.git #将github上项目克隆到本地
git push -u origin master     # 推送本地 master 去 origin
git remote -v #查看当前远程库
git remote add origin https://github.com/JustLikeY/scrum.git #与远程建立连接,origin是远程仓库在你本地的名称，可以根据自己的喜好更改
git pull #抓取远程更新
```

# 后悔药（撤销、补交、删除、移动）

```shell
#删除git中的文件（执行后提交方可生效）
git rm <file>
#移动文件（执行后提交方可生效）
git mv file_from file_to
#还原(还原到最后一次提交状态)
git checkout -- <file>
#将staged移动到工作区
git reset HEAD <file>
#补交（修改前次提交说明、补充遗漏提交）
git commit --amend
#回到e388136版本
git reset --hard e388136 
#查看e388136版本
git checkout d10425f -- 1.txt
```

# 分支

```shell
git branch dev    # 建立 dev 分支
git branch        # 查看当前分支有哪些
git checkout dev  #切换到dev分支
git checkout -b  dev     #创建并切换至分支dev
git commit -am "change 3 in dev"  # "-am": add 所有改变 并直接 commit
git merge dev         # 将 dev merge 到 当前分支 中
git merge --no-ff -m "keep merge info" dev   #将devmerge到master中并且在$git log --oneline --graph中能看到合并的分支图案
git stash #在分支a完成任务A时，突然来个任务B，此时需要将任务A的内容保存起来
git stash list #查看当前分支上的stash缓存
git stash pop #导出当前分支上的stash缓存
git remote add origin https://github.com/JustLikeY/git.git
git push -u origin master     # 推送本地 master 去 origin

git branch -D branch-name #删除分支
```

# 对比（unstaged、staged、commit）

```shell
git diff --staged #暂存内容和上次提交对比
git diff #工作区和暂存内容对比
```

# 提交

```shell
git commit -m "提交说明"  #提交
git commit -am "提交说明" #跳过暂存区提交
```

>**提交前**分支合并流程：
>
>1.合并分支之前先将当前分支的history清理好，同一个功能的多次提交合并成一次,使用reset将head重置，然后重新提交
>
>2.将主分支合并到当前分支
>
>3.发MR

# 查看日志

```shell
git reflog #显示所有HEAD移动产生的日志
git log --oneline #只显示提交产生日志
```
# Git全局配置

### git status 文件名中文显示

```shell
git config --global core.quotepath false
```

# git常见问题

## 中文乱码

### git status文件目录乱码

```
wjc@wjc-PC:~/Desktop/note$ git status
位于分支 master
您的分支与上游分支 'origin/master' 一致。
要提交的变更：
  （使用 "git reset HEAD <文件>..." 以取消暂存）

        修改：     InstallSystem/sys-config.md
        新文件：   "Tool/Maven-\345\237\272\346\234\254\346\246\202\345\277\265.md"
```

1. 问题原因：core.quotepath的作用是控制路径是否编码显示的选项。当路径中的字符大于0x80的时候，如果设置为true，转义显示；设置为false，不转义。
2. 解决方法：执行 `git config --global core.quotepath false`







