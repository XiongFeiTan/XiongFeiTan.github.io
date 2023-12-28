---
layout: post
title: 关于Embedding一点总结
categories: [深度学习]
comments: true
description: 在深度学习中构建用户或者物品的Embedding是很常见的操作，那么Embedding是什么?
---

# Embedding
## 1. 前置
💡 在深度学习中，构建用户或者物品的**Embedding**是很常见的操作，那么 embedding是什么？以及在各种深度学习框架当中是如何做的呢？

## 2. 什么是Embedding
💡 词向量，英文名叫 **Word Embedding**，按照字面的意思，应该是词嵌入。说到词向量，首先想到的一般都是的 **Word2Vec**将词ID映射为向量。如我们知道RNN无法直接处理单词，因此需要通过某种方法把单词变成数字形式的向量才能作为RNN的输入。这种把单词映射到向量空间中的一个向量的做法称为词嵌入word embedding，对应的向量称为词向量word vector。

我们知道**one hot型的矩阵相乘，就像是相当于查表**，于是 embedding 它直接用查表作为操作，而不写成矩阵再运算，这大大降低了运算量。再得到了全连接层的参数之后，直接用这个全连接层的参数作为特征，或者用这个全连接层的参数作为字、词的表示，从而得到了字、词向量。同时能够发现了一些有趣的性质，比如向量的欧氏距离、夹角余弦能够在某种程度上表示字、词的相似度。

那为什么这些字词向量会有这样一些性质呢？
因为，我们在用语言模型无监督训练时，是开了窗口的，通过前N个字预测下一个字的概率，这个N就是窗口的大小，同一个窗口内的词语，会有相似的更新，这些更新会累积，而具有相似模式的词语就会把这些相似更新累积到可观的程度。

## 3. Embedding层基础使用与理解
💡 在pytorch、Keras、paddlepaddle之类的框架有一个Embedding层。这里以pytorch当中的embedding层为例：
`torch.nn.Embedding`
关于torch.nn.Embedding的理解，基础的参数有两个（num_embeddings, embedding_dim）
num_embeddings代表一共有多少个词, embedding_dim代表你想要为每个词创建一个多少维的向量来表示它。

`import torch`
`from torch import nn`
`torch.manual_seed(0)`
`emb = nn.Embedding(10, 3)`
`emb.weight`
Embedding层中只有一个参数 weight，在创建时它会从标准正态分布中进行初始化.

其中全部参数:num_embeddings, embedding_dim, padding_idx=None, max_norm=None, norm_type=2.0, scale_grad_by_freq=False, sparse=False, _weight=None, _freeze=False, device=None, dtype=None 参考官方文档

**nn.Embedding 与 nn.Linear** 区别在于 
1. nn.Linear 接受向量作为输入，而 nn.Embedding 则是接受离散的索引作为输入；
2. nn.Embedding 实际上就是输入为 one-hot 向量，且不带bias 的 nn.Linear。
3. nn.Linear 在运算过程中做了矩阵乘法，而 nn.Embedding 是直接根据索引查表，因此在该情景下 nn.Embedding 的效率显然更高。



## 4. Embedding层更新问题
💡 nn.Embedding 的权重实际上就是词嵌入本身
nn.Embedding.weight 在更新的过程中既没有采用 Skip-gram 也没有采用 CBOW。
可以简单把 nn.Embedding 视为一个特殊的 nn.Linear 后，其更新机制就很好理解了，同样就是按照梯度进行更新罢了。训练结束后，得到的词嵌入是最适合当前任务的词嵌入，而非像**word2vec，GloVe**这种更为通用的词嵌入。当不想让向量在训练过程中自我更新，那么可以尝试冻结梯度，即：
`emb.weight.requires_grad = False`



### 5. 阅读文档
1. https://pytorch.org/docs/stable/generated/torch.nn.Embedding.html#torch.nn.Embedding
<br>
2. https://stackoverflow.com/questions/65445174/what-is-the-difference-between-an-embedding-layer-with-a-bias-immediately-afterw/65448744#65448744
<br>
3. https://stackoverflow.com/questions/50747947/embedding-in-pytorch
<br> 