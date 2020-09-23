# 项目创建

## IDEA创建

```
mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate -DarchetypeGroupId=org.apache.flink -DarchetypeArtifactId=flink-quickstart-java -DarchetypeVersion=${1:-1.10-SNAPSHOT} -DgroupId=org.myorg.quickstart -DartifactId=$PACKAGE -Dversion=0.1 -Dpackage=org.myorg.quickstart -DinteractiveMode=false -DarchetypeCatalog=https://repository.apache.org/content/repositories/snapshots/
```