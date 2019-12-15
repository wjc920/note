通常Kafka消息只支持至少写入一次，事务和幂等是为了支持Exactly Once

###### 幂等

每个生产者实例在初始化时会被分配一个PID（对用户透明），生产者每发送一条消息就会将<PID, 分区>对应的序列号+1，broker端同时也会维护一张<PID, 分区>表，每次收到消息都会验证（Producer端的序列号叫SN_new，broker端的序列号叫SN_old）：

- 如果SN_new=SN_old+1，broker接收消息

- 如果SN_new<SN_old+1，broker忽略消息

- 如果SN_new>SN_old+1，broker忽略消息，对应producer端会抛乱序异常

幂等只能保证单个生产者单分区的Exactly Once。

###### 事务

1. 找到事务控制器（TransactionCoordinator），事务控制器在_transaction_state中transactionId所对应分区的leader副本所在broker
2. 获取PID
3. 开启事务，真正开启事务是在第一条消息发送之时，同时将消息所在分区信息持久化到对应的PID持久化消息中
4. 提交/回滚事务，当produce端提交请求后，在broker端会首先提交PREPARE_COMMIT/PREPARE_ABORT消息，然后将COMMIT / ABORT消息写入到对应的topic和\_consumer_offset，最后将COMPLETE_COMMIT / COMPLETE_ABORT写入到\_transaction_state中，至此，事务处理完成。

