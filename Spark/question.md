# Q

- Spark闭包和Scala闭包的区别与联系？
- Spark withScope是什么？
- Spark中Application是什么？有什么用？
- 任务提交
  - DAGScheduler中
- 调度器（DAGScheduler）在什么时候启动？

# Concept

- SparkContext和Application是一一对应的关系
- 


# Spark Core包含哪些功能？

- 任务调度
- 内存管理
- 错误恢复
- 与存储系统交互

# 如何看待Spark中的行动算子？

Spark中的DAG图实际上是由RDD调用链组成，只有当调用链执行到Action RDD时才会触发代码的提交操作，代码提交之后才会得到真正的执行。这种惰性计算主要体现在shell模式下，而在使用Application模式下，这种特性并不明显。

