# 常用命令
| 命令 | 作用 |
| --- | ---|
| mvn help:effective-pom | 查看实际生效的pom文件 |

# Maven基本概念
- Maven的唯一作用是解析pom文件，其余人均都由插件来完成。
- Maven提倡统一的标注、统一的项目布局、统一的生命周期、标准的仓库格式
- Maven&Ant：Maven规定一组约定（源码的位置、编译文件的位置）和生命周期，而Ant没有规定，所以需要显示声明，特别复杂
- Ant适合高度自定义构建的项目，Maven适合构建标准的项目,两者可以结合使用
- Maven最高效的方式永远是命令行

# POM

## 超级POM

|  Maven版本   | Jar位置  |
|  ----  | ----  |
| Maven2  | ＄MAVEN_HOME/lib/maven-model-builder-x.x.x.jar |
| Maven3  | ＄MAVEN_HOME/lib/maven-x.x.x-uber.jar |

## 聚合

聚合类型的项目和普通项目的pom文件之间的差别（以project0聚合project1和project2为例）：

- packaging为pom
- 新增modules标签

  ```
  <modules>
    <module>project1</module>
    <module>project2</module>
  </modules>
  ```

> project1和project2不是必须在project0目录下，也可以平行，如果三个项目在同一个目录下时，modules需要修改为：
> ```
> <modules>
>   <module>../project1</module>
>   <module>../project2</module>
> </modules>
> ```

## 继承

### 可以继承的元素

- groupId：项目组ID，项目坐标的核心元素。

- version：项目版本，项目坐标的核心元素。

- description：项目的描述信息。

- organization：项目的组织信息。

- inceptionYear：项目的创始年份。

- url：项目的URL地址。

- developers：项目的开发者信息。

- contributors：项目的贡献者信息。

- distributionManagement：项目的部署配置。

- issueManagement：项目的缺陷跟踪系统信息。

- ciManagement：项目的持续集成系统信息。

- scm：项目的版本控制系统信息。

- mailingLists：项目的邮件列表信息。

- properties：自定义的Maven属性。

- dependencies：项目的依赖配置。

- dependencyManagement：项目的依赖管理配置。

- repositories：项目的仓库配置。

- build：包括项目的源码目录配置、输出目录配置、插件配置、插件管理配置等。

- reporting：包括项目的报告输出目录配置、报告插件配置等。- groupId：项目组ID，项目坐标的核心元素。

- version：项目版本，项目坐标的核心元素。

- description：项目的描述信息。

- organization：项目的组织信息。

- inceptionYear：项目的创始年份。

- url：项目的URL地址。

- developers：项目的开发者信息。

- contributors：项目的贡献者信息。

- distributionManagement：项目的部署配置。

- issueManagement：项目的缺陷跟踪系统信息。

- ciManagement：项目的持续集成系统信息。

- scm：项目的版本控制系统信息。

- mailingLists：项目的邮件列表信息。

- properties：自定义的Maven属性。

- dependencies：项目的依赖配置。

- dependencyManagement：项目的依赖管理配置。

- repositories：项目的仓库配置。

- build：包括项目的源码目录配置、输出目录配置、插件配置、插件管理配置等。

- reporting：包括项目的报告输出目录配置、报告插件配置等。

### dependencies


# Maven配置

[settings.xml相关的配置教程地址](https://maven.apache.org/settings.html)

## 代理配置

适用场景：有时候你所在的公司基于安全因素考虑，要求你使用通过安全认证的代理访问因特网。这种情况下，就需要为Maven配置HTTP代理，才能让它正常访问外部仓库，以下载所需要的资源。

解决方法：编辑~/.m2/settings.xml文件，修改如下内容

```
<proxy>
    <id>optional</id>
    <active>true</active>
    <protocol>http</protocol>
    <username>proxyuser</username>
    <password>proxypass</password>
    <host>proxy.host.net</host>
    <port>80</port>
    <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
</proxy>
```

## 修改JVM堆大小

- maven所有版本通用：
  - Linux：在mvn中添加`MAVEN_OPTS=-Xms256m -Xmx768m -XX:PermSize=128m -XX:MaxPermSize=256M`
  - Windows：在mvn.bat中添加`set MAVEN_OPTS=-Xms256m -Xmx768m -XX:PermSize=128m -XX:MaxPermSize=256M`
- maven3.3.1+：添加`-Xmx2048m -Xms1024m -XX:MaxPermSize=512m -Djava.awt.headless=true`到`${maven.projectBasedir}/.mvn/jvm.config`文件中，可以实现每个项目单独配置

# Maven远程仓库

## 远程仓库种类

- 本地仓库
- 远程仓库
  - 中央仓库
  - 私服
  - 其他公共仓库

## 远程仓库的认证

在settings.xml文件中，配置servers->server相关配置，可以配置用户名密码登录、私钥方式登录，其中ID要和仓库ID对应。

## 快照版本

```shell
mvn clean install -U # 强制更新RELEASE、LATEST和SNAPSHOT
```

## 关于Nexus

仓库的种类：

- 宿主库（hosted）：企业内部公用Jar存放的位置
- 代理库（proxy）：缓存开源Jar
- 仓库组（group）：包含一组宿主库、代理库，在maven客户端只需要配置仓库组的地址就可以访问组内各个库的Jar


# 思考问题

- Maven是干什么的？

  > Maven是用来管理项目的，清理、编译、测试、打包、发布，以及一些自定义的过程本身就是一件复杂的事情。

- 继承和依赖的区别

# 兴趣点

- 使用finalName控制mvn clean package输出的jar、war包名称
- 

第一列：第一依赖   第一行：第二依赖
|  | compile | test | provided | runtime |
|:--:|:--:|:--:|:--:|:--:|
| **compile** | compile | - | - | runtime |
| **test** | test | - | - | test |
| **provided** | provided | - | provided | provided |
| **runtime** | runtime | - | - | runtime |




