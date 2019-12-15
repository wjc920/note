###### kafka是真正意义上的高可扩展的，topic可以通过partition来横向扩展

- 优点：增加单个topic的吞吐，支撑任何体量的topic

- 缺点：会导致topic消息乱序（在produce端设置好分区规则，可以有效解决该特性，实在不行只好采用单partition了）

###### Kafka和RocketMQ的备份机制

- Kafka：对每个分区都可以专门设置多副本机制，灵活，且分布式备份足够可靠
- 



###### Consumer端

- Kafka采用短轮寻的方式，实时性取决于轮寻的速度