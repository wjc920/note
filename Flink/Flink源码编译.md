# pom修改
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
mvn clean install -DskipTests -Drat.skip=true