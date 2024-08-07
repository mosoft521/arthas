---
id: "question-history-15731"
title: "artahs 过滤方法的阐述"
date: "2024-07-04"
category: "expertConsultation"
description: "Arthas 提供了强大的方法调用监控与分析功能，其中在监控方法执行时，能够实现根据特定条件（如执行耗时或自定义条件表达式）来过滤统计结果，这有助于快速定位和诊断性能瓶颈或异常调用。下面我将依据提供的知识内容，对 Arthas 过滤方法的机制进行阐述：### 1. 按耗时过滤方法执行在 Arthas"
---

## 用户问题 ：

artahs 过滤方法的阐述

---

## 专家官方解答 ：

Arthas 提供了强大的方法调用监控与分析功能，其中在监控方法执行时，能够实现根据特定条件（如执行耗时或自定义条件表达式）来过滤统计结果，这有助于快速定位和诊断性能瓶颈或异常调用。下面我将依据提供的知识内容，对 Arthas 过滤方法的机制进行阐述：

### 1. 按耗时过滤方法执行

在 Arthas 中，可以使用 `watch`、`stack` 和 `trace` 命令时添加 `#cost` 条件来过滤方法执行的统计信息。例如，`#cost>200` 表示仅展示执行耗时超过 200 毫秒的方法调用记录。这对于识别偶尔出现的性能问题特别有用，因为它帮助开发者聚焦于那些响应时间异常长的调用路径，而忽略常态下的快速执行情况。

**执行示例**:

```bash
watch demo.MathGame primeFactors '{params, returnObj}' '#cost>200' -x 2
```

此命令会监视 `demo.MathGame` 类中 `primeFactors` 方法的调用，当其执行耗时超过 200 毫秒时，输出调用参数及返回对象，并且 `-x 2` 参数表示跳过前两次调用来忽略初始化等非典型调用情况。

### 2. 计算条件表达式过滤统计结果

此外，`monitor` 命令允许在方法执行完毕后，基于自定义条件表达式来过滤和统计调用结果。例如，`"params[0] <= 2"` 表示仅当方法的第一个参数不大于 2 时，才记录这次调用的统计信息。

**执行示例**:

```bash
monitor -c 5 demo.MathGame primeFactors "params[0] <= 2"
```

这里，每 5 秒收集一次数据，仅统计满足条件 `params[0] <= 2` 的 `primeFactors` 方法调用情况，包括调用次数、成功率、失败率等关键指标。

### 解释

通过这些功能，开发者能够灵活地定制监控策略，针对不同场景下性能分析和故障排查的需求，实现高效的问题定位。耗时过滤直接帮助识别慢调用，而条件表达式过滤则适用于更细致的业务逻辑匹配，两者结合可以提供全面的方法监控解决方案。

### 注意

请确保理解所使用的过滤条件，正确设置以避免错过重要信息或引入误报。同时，合理利用 `-x` 参数（跳过初始调用）和监控频率（如 `-c` 参数），以获取最准确的监控数据。

综上所述，Arthas 的方法过滤功能通过条件化的执行耗时和自定义表达式，为 Java 应用的性能监控和问题诊断提供了强大而灵活的工具。

<font color="#949494">---------------</font>

## 参考链接 ：

\*[# watch](https://github.com/alibaba/arthas/tree/master/site/docs/doc/watch.md)

\*[### Arthas3.0 的新特性](https://github.com/alibaba/arthas/tree/master/site/docs/doc/arthas3.md)

\*[# monitor](https://github.com/alibaba/arthas/tree/master/site/docs/doc/monitor.md)

<font color="#949494">---------------</font>

## <font color="#FF0000">答疑服务说明：</font>

本内容经由技术专家审阅的用户问答的镜像生成，我们提供了<font color="#FF0000">专家智能答疑服务</font>，在<font color="#FF0000">页面的右下的浮窗”专家答疑“</font>。您也可以访问 : [全局专家答疑](https://answer.opensource.alibaba.com/docs/intro) 。 咨询其他产品的的问题

### 反馈

如问答有错漏，欢迎点：[差评](https://ai.nacos.io/user/feedbackByEnhancerGradePOJOID?enhancerGradePOJOId=16091)给我们反馈。
