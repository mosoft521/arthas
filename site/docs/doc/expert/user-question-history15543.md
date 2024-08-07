---
id: "question-history-15543"
title: "arthas中tt命令如何查看方法入参的具体命令"
date: "2024-07-04"
category: "expertConsultation"
description: "在Arthas中，`tt`命令用于记录指定方法每次调用的入参和返回信息，并能够对这些不同时间点的调用进行观测。要查看方法入参的具体命令，你可以按照以下步骤操作：1. **启动`tt`命令**：首先，你需要确定想要观察的方法及其所在类的全限定名。假设你要观察的是`com.example.MyClass"
---

## 用户问题 ：

arthas中tt命令如何查看方法入参的具体命令

---

## 专家官方解答 ：

在Arthas中，`tt`命令用于记录指定方法每次调用的入参和返回信息，并能够对这些不同时间点的调用进行观测。要查看方法入参的具体命令，你可以按照以下步骤操作：

1. **启动`tt`命令**：首先，你需要确定想要观察的方法及其所在类的全限定名。假设你要观察的是`com.example.MyClass`类中的`myMethod`方法，可以使用以下命令启动`tt`监控：

   ```shell
   tt com.example.MyClass myMethod
   ```

   这将开始记录指定方法的所有调用情况，包括入参和返回值。

2. **查看记录**：执行上述命令后，`tt`会分配一个ID给这次跟踪任务。你可以通过这个ID来查看具体某次调用的详情。当你想要查看记录时，可以使用`tt -i <task-id>`命令，其中`<task-id>`是你从上一步骤中获得的任务ID。

   ```shell
   tt -i <task-id>
   ```

3. **分析入参**：上述命令将会展示指定跟踪任务的所有调用记录，每条记录中包含了调用时间戳、入参以及返回值等详细信息。你可以直接在输出中找到并分析你感兴趣的入参。

4. **停止追踪**：在完成观测后，为了减少资源占用，你可以选择停止特定的追踪任务或所有追踪任务。停止特定任务使用：

   ```shell
   tt -i <task-id> --stop
   ```

   而停止所有`tt`任务可以执行：

   ```shell
   tt --all --stop
   ```

**解释**：`tt`命令通过在JVM级别记录方法调用的元数据，提供了强大的动态跟踪能力，这对于诊断方法调用异常、性能瓶颈或是理解复杂系统的行为非常有帮助。需要注意的是，尽管`tt`功能强大，但由于其记录的详细程度，可能会对应用性能产生一定影响，因此建议在非生产环境或者问题复现阶段谨慎使用，并及时清理不再需要的跟踪任务。

<font color="#949494">---------------</font>

## 参考链接 ：

\*[# 命令列表](https://github.com/alibaba/arthas/tree/master/site/docs/doc/commands.md)

\*[# Http API](https://github.com/alibaba/arthas/tree/master/site/docs/doc/http-api.md)

<font color="#949494">---------------</font>

## <font color="#FF0000">答疑服务说明：</font>

本内容经由技术专家审阅的用户问答的镜像生成，我们提供了<font color="#FF0000">专家智能答疑服务</font>，在<font color="#FF0000">页面的右下的浮窗”专家答疑“</font>。您也可以访问 : [全局专家答疑](https://answer.opensource.alibaba.com/docs/intro) 。 咨询其他产品的的问题

### 反馈

如问答有错漏，欢迎点：[差评](https://ai.nacos.io/user/feedbackByEnhancerGradePOJOID?enhancerGradePOJOId=16086)给我们反馈。
