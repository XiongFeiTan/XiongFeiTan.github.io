---
layout: post
title: Spark ML Pipeline
categories: [机器学习]
comments: true
description: 推荐使用基于Spark DataFrame ML开发传统机器学习任务
---

## Spark ml Pipeline

在Spark实践当中，DataFrames提供了比RDD更加友好的API，DataFrame的许多优点包括Spark DataSource，SQL / DataFrame查询，Tungsten和Catalyst优化以及跨语言的统一API等, 所以建议将以往基于RDD转换至DataFrame,可以我们带来性能上部分的优化。

---
其中ML当中的pipeline 借鉴于python的机器学习库scikit-learn中的Pipeline思想，统一API使用, 作为一个串连者, 把整个机器学习流程跑在一起, 更加方便的完成特定的开发流程。

--- 

主要包含如下几个部分：

> **Transformer**:一个Transformer相当于一个算法，可以将一个DataFrame转换为另一个DataFrame(如将一个带特征值的DataFrame转换为带预测值的DataFrame);

> **Estimator**：Estimator在一个DataFrame上完成Transformer转换过程。如一个学习算法就是一个Estimator，该Estimator应用在测试DataFrame上，
            完成模型的训练过程;

> **Param**：全部Transformers和 Estimators 共享通用的API，以完成各自特定参数的设置;

> **Pipeline**：将多个Transformers和 Estimators 串在一起，以完成某个特定的机器学习工作流程;

---

**具体的demo可以参考：**
1. 官方文档：```http://spark.apache.org/docs/latest/ml-pipeline.html```
