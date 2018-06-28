---
layout: post
title: TensorFlow 变量
date: 2018-05-08
categories: 深度学习
tags: [TensorFlow]
---

> 摘要：【未完待续】本文主要总结 TensorFlow 中变量的使用。

# 变量初始化

在 TensorFlow 中使用，`tf.Variable()` 来构建一个变量的初始化值，这个值可以是任意类型和任意维度的大小的张量。

如果我们再初始化一个变量值时需要用到另外一个变量，可以通过 `initialized_value()` 获取其他变量的值。

```
import numpy

# TensorFlow 的变量在使用前必须初始化，而常量不需要
v1 = tf.Variable(0.01)
v2 = tf.Variable(v1.initialized_value() * 2)


init = tf.global_variables_initializer()
with tf.Session() as sess:
	sess.run(init)
	sess.run(v1)
	sess.run(v2)

```

当进行训练的时候，有的变量是机器学习训练的参数，他们的值会在训练的过程中在梯度更新的时候发生改变，而有些值不属于机器学习训练的参数。我们再声明变量的时候，可以指定参数的 `trainable` 属性的布尔值来决定该变量的值是否能被更新。

```
import numpy

# 默认 trainable 为 true，表示可以被更新
v1 = tf.Variable(0.01, name="weight")   

# 这个变量不会被更新
v2 = tf.Variable(v1.initialized_value() * 2, name="step", trainable=False) 
```

# 变量变形

在构建完变量之后，变量的类型和维度大小就固定了。之后如果要强制改变变量的维度大小，可以采用 reshape 操作来改变变量的维度。

```
import numpy

v1 = tf.Variable([1, 2, 3, 4, 5, 6, 7, 8, 9])
reshaped_v2 = tf.reshape(v1, [3, 3])

```

# 共享变量和共享命名空间


