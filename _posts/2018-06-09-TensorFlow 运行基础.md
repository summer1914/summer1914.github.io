---
layout: post
title: TensorFlow 运行基础
date: 2018-05-08
categories: 深度学习
tags: [TensorFlow]
---

> 摘要：本文主要总结 TensorFlow 的运行结构。

# 框架运行结构

- 用张量 tensor 表示数据
- 计算图 graph 表示任务
- 在会话 session 中执行 context
- 通过变量维护状态
- 通过 feed 和 fetch 可以任意的操作数据

# Numpy 和 TensorFlow 中的张量

| Numpy | TensorFlow |
| --- | --- |
| `a = np.zeros((2,2));b = np.ones((2,2))` | `a = tf.zeros((2,2)); b = tf.ones((2,2))` |
| `np.sum(b, axis=1)`| `tf.reduce_sum(a, reduction_indices=[1])` |
| `a.shape`| `a.get_shape()` |
| `np.reshape(1, (1, 4))` |`tf.reshape(1, (1, 4))` |
| `b*5 + 1` | `b*5+1` |
| `np.dot(a, b)` | `tf.matmul(a, b)`|
| `a[0,0], a[:0], a[0,:]`| `a[0,0], a[:0], a[0,:]` |
|`print a`|`print a.eval()`|


# Demo

``` Python
# -*- coding: utf-8 -*-

import tensorflow as tf
from tensorflow.examples.tutorials.mnist import input_data

sess = tf.InteractiveSession()
minist = input_data.read_data_sets('MNIST_data', one_hot=True)

# 输入节点
x = tf.placeholder(tf.float32, shape=[None, 784])
y_ = tf.placeholder(tf.float32, shape=[None, 10])

# 参数和变量
W = tf.Variable(tf.zeros([784, 10]))
b = tf.Variable(tf.zeros([10]))

# 运算节点
y = tf.nn.softmax(tf.matmul(x, W) + b)
cross_entropy = -tf.reduce_sum(y_ * tf.log(y))

# 优化
train_step = tf.train.GradientDescentOptimizer(0.01).minimize(cross_entropy)

# 初始化变量
sess.run(tf.initialize_all_variables())

# 训练过程
for i in xrange(5000):
    batch = minist.train.next_batch(32)
    train_step.run(feed_dict={x: batch[0], y_: batch[1]})
    if i % 100 == 0:
        loss = cross_entropy.eval(feed_dict={x: batch[0], y_: batch[1]})
        print("====> %g" % loss)

correct_prediction = tf.equal(tf.argmax(y, 1), tf.argmax(y_, 1))
accuracy = tf.reduce_mean(tf.cast(correct_prediction, tf.float32))

print(accuracy.eval(feed_dict={x: minist.test.images, y_: minist.test.labels}))

```
