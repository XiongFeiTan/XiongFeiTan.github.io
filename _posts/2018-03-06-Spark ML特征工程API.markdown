---
layout: post
title: Spark ML特征工程API
categories: [机器学习]
comments: true
description: Spark ML中部分常用特征工程相关API简单解释
---

**Spark Ml 部分常用API解析：**

>  1.**VectorAssembler** 将部分列的数据转换为特征向量，统一命名。

> 2.**QuantileDisretizer** 将连续型特征转换为分级特征，分级数量由numBuckets参数决定。

```scala
例子：
val transformer = new QuantileDiscretizer()
.setInputCol("xxx")
.setOutputCol("yyy")
.setNumBuckets(3)
```

> 3.**ElementwiseProduct** 按提供的weight(权重)向量，返回与输入向量元素级别的乘积，一一对应。

```scala
val transformer = new ElementwiseProduct()
  .setScalingVec("weightvectorinput")
  .setInputCol("vector")
  .setOutputCol("transformedVector")
```

> 4.**MaxAbsScaler** 使用每个特征的最大值的绝对值将输入向量的特征值转换到[-1,1]之间。

> 5.**StandardScaler** 处理Vector数据，标准化每个特征使得其有统一的标准差以及（或者）均值为零。

> 6.**MinMaxScaler**  通过重新调节大小将Vector形式的列转换到指定的范围内，通常为[0,1]，它的参数有。

> 7.**Normalizer**  一个转换器，它可以将多行向量输入转化为统一的形式。

> 8.**VectorIndexer** 转化数据集中的类别特征Vector.

> ...
