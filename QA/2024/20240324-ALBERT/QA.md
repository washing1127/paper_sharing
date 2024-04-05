# Transformer中的参数共享

**Transformer 论文 -> 第3章 Model Architecture -> 3.4节 Embeddings and Softmax**

```
Similarly to other sequence transduction models, we use learned embeddings to convert the input tokens and output tokens to vectors of dimension $d_{model}$. 

We also use the usual learned linera transformation and softmax function to convert the decoder output to predicted next-token probabilities.

In our model, we **share the same weight matrix between the two embeddings layers and the pre-softmax linear transformation**, similar to 1608.05859
```

[1608.05859](https://arxiv.org/abs/1608.05859) 中的参数共享主要指input embedding和outpu embedding之间的共享，他初始化一个embedding同时用于input和output。训练时input和output一同更新，保持不变。

transformer中的共享更多地体现在multi-head attention机制，以及position encoding中。多头注意力部分，同一层多个头之间QKV矩阵不相同，不同层中对应的同一个头的QKV矩阵相同。position encoding在不同层中也是一样的。

# DQE那里提到的那句话是什么意思
> DQE can reach an equilibrium point for which the input embedding and the output embedding of a certain layer stay the same.

就是字面意义上的，DQE可以达到某一层输入和输出是一样的，也就意味着这一层对模型的最终预测是没有帮助的，同样也就意味着模型已经得到了充分的训练，再增加额外的隐藏层数也不能增加模型的表达能力了。

# ALBERT 和 BERT 在训练数据上有什么差异

BERT和ALBERT的训练数据量是相似的，ALBERT主要讨论的目标是减少模型参数量和计算成本，而不是增加与训练数据的量。
