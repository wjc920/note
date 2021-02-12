# pom修改

在国内，由于部分Jar包无法下载，删除部分依赖才能顺利编译Flink项目。如果编译主机开启VPN代理能正常访问外网，POM文件可不做任何修改。

```xml
pom.xml
  <module>flink-runtime-web</module>
flink-connectors\pom.xml
  <module>flink-connector-gcp-pubsub</module>
flink-formats\pom.xml
  <module>flink-avro-confluent-registry</module>
flink-end-to-end-tests\pom.xml
  <module>flink-confluent-schema-registry</module>
  <module>flink-connector-gcp-pubsub-emulator-tests</module>
flink-examples\flink-examples-build-helper\pom.xml
  <module>flink-examples-streaming-gcp-pubsub</module>
```

# 执行编译命令
mvn clean install -DskipTests -Drat.skip=true -Dcheckstyle.skip=true


# 常见问题

## 1 

1. 问题描述  

```
严重: Step 'google-java-format' found problem in 'src\main\java\org\apache\flink\annotation\docs\ConfigGroup.java':
Unable to resolve dependencies
com.diffplug.spotless.maven.ArtifactResolutionException: Unable to resolve dependencies
        at com.diffplug.spotless.maven.ArtifactResolver.resolveDependencies(ArtifactResolver.java:88)
        at com.diffplug.spotless.maven.ArtifactResolver.resolve(ArtifactResolver.java:74)
        at com.diffplug.spotless.JarState.provisionWithTransitives(JarState.java:68)
        at com.diffplug.spotless.JarState.from(JarState.java:57)
        at com.diffplug.spotless.JarState.from(JarState.java:52)
        at com.diffplug.spotless.java.GoogleJavaFormatStep$State.<init>(GoogleJavaFormatStep.java:123)
        at com.diffplug.spotless.java.GoogleJavaFormatStep.lambda$create$0(GoogleJavaFormatStep.java:75)
        at com.diffplug.spotless.FormatterStepImpl.calculateState(FormatterStepImpl.java:56)
        at com.diffplug.spotless.LazyForwardingEquality.state(LazyForwardingEquality.java:56)
        at com.diffplug.spotless.FormatterStep$Strict.format(FormatterStep.java:76)
        at com.diffplug.spotless.Formatter.compute(Formatter.java:230)
        at com.diffplug.spotless.PaddedCell.calculateDirtyState(PaddedCell.java:201)
        at com.diffplug.spotless.PaddedCell.calculateDirtyState(PaddedCell.java:188)
        at com.diffplug.spotless.maven.SpotlessCheckMojo.process(SpotlessCheckMojo.java:52)
        at com.diffplug.spotless.maven.AbstractSpotlessMojo.execute(AbstractSpotlessMojo.java:146)
        at com.diffplug.spotless.maven.AbstractSpotlessMojo.execute(AbstractSpotlessMojo.java:137)
        at org.apache.maven.plugin.DefaultBuildPluginManager.executeMojo(DefaultBuildPluginManager.java:137)
        at org.apache.maven.lifecycle.internal.MojoExecutor.execute(MojoExecutor.java:210)
        at org.apache.maven.lifecycle.internal.MojoExecutor.execute(MojoExecutor.java:156)
        at org.apache.maven.lifecycle.internal.MojoExecutor.execute(MojoExecutor.java:148)
        at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject(LifecycleModuleBuilder.java:117)
        at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject(LifecycleModuleBuilder.java:81)
        at org.apache.maven.lifecycle.internal.builder.singlethreaded.SingleThreadedBuilder.build(SingleThreadedBuilder.java:56)
        at org.apache.maven.lifecycle.internal.LifecycleStarter.execute(LifecycleStarter.java:128)
        at org.apache.maven.DefaultMaven.doExecute(DefaultMaven.java:305)
        at org.apache.maven.DefaultMaven.doExecute(DefaultMaven.java:192)
        at org.apache.maven.DefaultMaven.execute(DefaultMaven.java:105)
        at org.apache.maven.cli.MavenCli.execute(MavenCli.java:957)
        at org.apache.maven.cli.MavenCli.doMain(MavenCli.java:289)
        at org.apache.maven.cli.MavenCli.main(MavenCli.java:193)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.codehaus.plexus.classworlds.launcher.Launcher.launchEnhanced(Launcher.java:282)
        at org.codehaus.plexus.classworlds.launcher.Launcher.launch(Launcher.java:225)
        at org.codehaus.plexus.classworlds.launcher.Launcher.mainWithExitCode(Launcher.java:406)
        at org.codehaus.plexus.classworlds.launcher.Launcher.main(Launcher.java:347)
Caused by: org.eclipse.aether.resolution.DependencyResolutionException: Could not transfer artifact com.google.errorprone:javac-shaded:jar:9+181-r4173-1 from/to al
iyun (http://maven.aliyun.com/nexus/content/groups/public/): Authorization failed for http://maven.aliyun.com/nexus/content/groups/public/com/google/errorprone/jav
ac-shaded/9+181-r4173-1/javac-shaded-9+181-r4173-1.jar 403 Forbidden
        at org.eclipse.aether.internal.impl.DefaultRepositorySystem.resolveDependencies(DefaultRepositorySystem.java:357)
        at com.diffplug.spotless.maven.ArtifactResolver.resolveDependencies(ArtifactResolver.java:86)
        ... 37 more
Caused by: org.eclipse.aether.resolution.ArtifactResolutionException: Could not transfer artifact com.google.errorprone:javac-shaded:jar:9+181-r4173-1 from/to aliy
un (http://maven.aliyun.com/nexus/content/groups/public/): Authorization failed for http://maven.aliyun.com/nexus/content/groups/public/com/google/errorprone/javac
-shaded/9+181-r4173-1/javac-shaded-9+181-r4173-1.jar 403 Forbidden
        at org.eclipse.aether.internal.impl.DefaultArtifactResolver.resolve(DefaultArtifactResolver.java:424)
        at org.eclipse.aether.internal.impl.DefaultArtifactResolver.resolveArtifacts(DefaultArtifactResolver.java:229)
        at org.eclipse.aether.internal.impl.DefaultRepositorySystem.resolveDependencies(DefaultRepositorySystem.java:340)
        ... 38 more
Caused by: org.eclipse.aether.transfer.ArtifactTransferException: Could not transfer artifact com.google.errorprone:javac-shaded:jar:9+181-r4173-1 from/to aliyun (
http://maven.aliyun.com/nexus/content/groups/public/): Authorization failed for http://maven.aliyun.com/nexus/content/groups/public/com/google/errorprone/javac-sha
ded/9+181-r4173-1/javac-shaded-9+181-r4173-1.jar 403 Forbidden
        at org.eclipse.aether.connector.basic.ArtifactTransportListener.transferFailed(ArtifactTransportListener.java:52)
        at org.eclipse.aether.connector.basic.BasicRepositoryConnector$TaskRunner.run(BasicRepositoryConnector.java:369)
        at org.eclipse.aether.util.concurrency.RunnableErrorForwarder$1.run(RunnableErrorForwarder.java:75)
        at org.eclipse.aether.connector.basic.BasicRepositoryConnector$DirectExecutor.execute(BasicRepositoryConnector.java:644)
        at org.eclipse.aether.connector.basic.BasicRepositoryConnector.get(BasicRepositoryConnector.java:262)
        at org.eclipse.aether.internal.impl.DefaultArtifactResolver.performDownloads(DefaultArtifactResolver.java:499)
        at org.eclipse.aether.internal.impl.DefaultArtifactResolver.resolve(DefaultArtifactResolver.java:401)
        ... 40 more
Caused by: org.apache.maven.wagon.authorization.AuthorizationException: Authorization failed for http://maven.aliyun.com/nexus/content/groups/public/com/google/err
orprone/javac-shaded/9+181-r4173-1/javac-shaded-9+181-r4173-1.jar 403 Forbidden
        at org.apache.maven.wagon.providers.http.wagon.shared.AbstractHttpClientWagon.fillInputData(AbstractHttpClientWagon.java:1180)
        at org.apache.maven.wagon.providers.http.wagon.shared.AbstractHttpClientWagon.fillInputData(AbstractHttpClientWagon.java:1138)
        at org.apache.maven.wagon.StreamWagon.getInputStream(StreamWagon.java:126)
        at org.apache.maven.wagon.StreamWagon.getIfNewer(StreamWagon.java:88)
        at org.apache.maven.wagon.StreamWagon.get(StreamWagon.java:61)
        at org.eclipse.aether.transport.wagon.WagonTransporter$GetTaskRunner.run(WagonTransporter.java:567)
        at org.eclipse.aether.transport.wagon.WagonTransporter.execute(WagonTransporter.java:435)
        at org.eclipse.aether.transport.wagon.WagonTransporter.get(WagonTransporter.java:412)
        at org.eclipse.aether.connector.basic.BasicRepositoryConnector$GetTaskRunner.runTask(BasicRepositoryConnector.java:457)
        at org.eclipse.aether.connector.basic.BasicRepositoryConnector$TaskRunner.run(BasicRepositoryConnector.java:364)
        ... 45 more
```

2. 问题原因

无法下载 `javac-shaded-9+181-r4173-1.jar` 包导致，真实原因未知，但猜测是我的mvn配置文件导致。

3. 解决方法

复制 `http://maven.aliyun.com/nexus/content/groups/public/com/google/errorprone/javac-shaded/9+181-r4173-1/javac-shaded-9+181-r4173-1.jar` 到浏览器，下载jar包，下载后放到，本地mvn仓库的 `com\google\errorprone\javac-shaded\9+181-r4173-1` 目录中，再次直接mvn编译命令即可。


  


