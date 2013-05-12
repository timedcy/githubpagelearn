---
layout: default
title: 神经网络
description: "Neural networks"
category: []
---

{% include JB/setup %}

神经网络
=====

##Neural networks的历史
* 1943年，McCulloch和Pitts建立了neuron的数学模型，$$ y=I\left(\Sigma _{i} w_{i} x_{i}>\theta \right) $$
* 1957年，Frank Rosenblatt发明perceptron learning algorithm
* 1969年，Bryson, A. 和Y.-C. Ho发现backpropagation algorithm
* 1986年，Rumelhart、Hinton和Williams发现backpropagation algorithm可以拟合有隐藏层的模型，并引起人们注意
* 1987年，Sejnowski和Rosenberg发明NETtalk，通过隐藏层将单词映射成语音元素，从而可以人工合成语音
* 1989年， Yann Le Cun等发明LeNet系统
* 1992年，Boser发明support vector machine，从此kernel方法流行
* 2002年，Geoff Hinton发明contrastive divergence training procedure（每层依次训练），首次可以处理深层网络，从而神经网络又流行

##Feedforward neural network
Feedforward neural network，或称multi-layer perceptron (MLP)，是logistic regression模型逐层叠加并在输出层用logistic regression或linear regression来实现的。

$$
\begin{align}
p\left( y | \mathbf{x}, \mathbf{\theta} \right) &= \mathcal{N} \left(y| \mathbf{w}^{T} \mathbf{z} \left( \mathbf{x} \right), \sigma^2 \right) \\
\mathbf{z} \left( \mathbf{x} \right) &= g \left( \mathbf{V} \mathbf{x} \right) = \left[ g \left( \mathbf{v}_{i}^{T} \mathbf{x} \right), ..., g \left( \mathbf{v}_{H}^{T} \mathbf{x} \right) \right]
\end{align}
$$

 $$ g $$ 是非线性activation或称transfer function (通常是logistic function)，$$ \mathbf{z} \left( \mathbf{x} \right) = \mathbf{\phi} \left( \mathbf{x}, \mathbf{V} \right) $$称hidden layer，$$ H $$是hidden units的数量，$$ \mathbf{V} $$是输入到隐藏层的权重矩阵，$$ \mathbf{w} $$是隐藏层到输出层的权重向量。如下图所示：
<CENTER><p><img src="{{ site.img_url }}/A neural network with one hidden layer.png" alt="A neural network with one hidden layer" /></p></CENTER>
##Backpropagation algorithm

不像广义线性模型(GLM)，MLP的NLL(negative log likelihood)是non-convex函数，但是可以通过gradient-based optimization方法找到局部的最优值。
MLP通常参数量大，而且训练数据量大，所以一般采用first-order online methods去训练，其又称为stochastic gradient descent方法。而GLM通常用IRLS(Iteratively reweighted least squares)来解，或者称second-order offline method。

Backpropagation算法根据微积分的链式法则求这个NLL的梯度向量。
