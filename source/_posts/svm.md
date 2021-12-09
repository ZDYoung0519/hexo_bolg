title: SVM原理即推导
date: 2021-12-08 16:31:21

cover: true

tags:
  - 机器学习
  - 支持向量机
categories:
  - 机器学习
plugins:
  - mathjax
  - katex
---
支持向量机算法介绍。

<!-- more -->

# 感知机简介
感知机由 Rosenlatt 在 1957 年提出，它用来模拟神经细胞的动作和行为。单个神经元细胞可以被视为两种状态：激活为”是”，未激活为“否”。
其学习机是如下函数：
$$f(x)=\text{sign}(\mathbf{w}^T\mathbf{x})$$

然而，感知机所得到的**最终的超平面不一定是唯一**的，这往往依赖于其初值和迭代次序的设置，从本质上来讲是因为，感知机仅仅寻求将数据完全正确划分的超平面，而不考虑其他的准则。此外，感知机算法**只能处理线性可分的数据**，对于线性不可分的问题，算法会反复跌宕无法收敛到准确解。


支持向量机算法的提出，对这两个问题进行了解决。Cortes 与 Vapnik 提出线性支持向量机，通过最大化硬间隔的方式解决最终平面不唯一的问题。而 Boser、Guyon 与 Vapnik通过引入核技巧，提出了非线性的支持向量机，来处理非线性可分数据。

# 线性支持向量机
在感知机中，同样是寻找超平面将数据进行分离，然而这样的超平面往往是**不唯一**的。
如下图，哪个超平面分类是最好的？
从直觉上来讲，黑色的超平面是最好的。因为蓝色超平面对于左侧的一个正类样本分类容易分错，而红色的超平面对于右侧的一个夫分类样本容易分错。
![在这里插入图片描述](https://img-blog.csdnimg.cn/33ea758737294187948ce80bd71a28d0.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA54eD54On55qE5rWF6JOdMjAyMQ==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
空间中的超平面方程可以表示为：
$$\mathbf{w}^T\mathbf{x}+b=0$$
若超平面能够将训练样本$(\mathbf{x}_i,y_i)$分类正确，即：若$y_i=+1$有$\mathbf{w}^T\mathbf{x}+b>0$；若$y_i=-1$有$\mathbf{w}^T\mathbf{x}+b<0$. 令
$$
\mathbf{w}^T\mathbf{x}+b\ge1,\quad y_i=+1;\\
\mathbf{w}^T\mathbf{x}+b\le1,\quad y_i=-1.
$$
上式成立，是由于对一个超平面$(\mathbf{w},b)$，总能将其进行缩放使得上式成立。

于是就得到了空间中三个平面，如图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/8b11206d861740d49ae5cb4ca7c4f3cf.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA54eD54On55qE5rWF6JOdMjAyMQ==,size_12,color_FFFFFF,t_70,g_se,x_16#pic_center)
支持向量机的思想就是最大化间隔（Large Margin），即
$$
\begin{aligned}
&\max_{\mathbf{w},b} \quad\frac{2}{||\mathbf{w}||}\\
&\text{s.t.}\quad y_i(\mathbf{w}^T\mathbf{x}_i+b)\ge1
\end{aligned}
$$

等价于

$$
\begin{aligned}
&\min_{\mathbf{w},b} \quad||\mathbf{w}||^2\\
&\text{s.t.}\quad y_i(\mathbf{w}^T\mathbf{x}_i+b)\ge1
\end{aligned}
$$