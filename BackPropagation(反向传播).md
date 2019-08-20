# 正向反向传播——梯度爆炸问题

## 简易模型

$$h_t = W_{hx}x_t + W_{hh}h_{t-1} \tag{1}$$

- 没有**激活函数**和**偏差项**

- $W_{hx} \in R^{h \times d}$和$W_{hh} \in R^{h \times h}$是隐藏层的权重参数（与RNN一节中的相似。）
- 设输出层的权重参数$W_{qh} \in R^{q \times h}$，则在t时间点的输出层变量$o_t \in R^{q}$，则

$$o_t = W_{qh}h_t. \tag{2}$$

- 设损失函数$l(o_t,y_t)$，损失函数，也称为目标函数：

$$L = \frac{1}{T}\sum_{t=1}^T l(o_t,y_t). \tag{3}$$


对以下三个部分求梯度，进行学习：

1. $W_{hx}$
2. $W_{hh}$
3. $W_{qh}$

根据他们在整个神经网络中的位置，通过借助$o_t$、$h_t$等使用反向传播进行计算。

---

1.对于$\frac{\partial{L}}{\partial{W_{qh}}} = \sum_{t=1}^{T}\frac{\partial{L}}{\partial{o_t}} h_t^T$

- $\frac{\partial{L}}{\partial{o_t}}$容易计算

---

2.对于$\frac{\partial{L}}{\partial{W_{hx}}} = \sum_{t=1}^{T}\frac{\partial{L}}{\partial{h_t}} x_t^T$  和  $\frac{\partial{L}}{\partial{W_{hh}}} = \sum_{t=1}^{T}\frac{\partial{L}}{\partial{h_t}} h_{t-1}^T$

- $\frac{\partial{L}}{\partial{h_t}}$可由链式法则，通过递推公式获得=$\sum_{i=t}^{T}(W_{hh}^{T})^{T-i}W_{qh}^T \frac{\partial{L}}{\partial{o_{T+t-i}}}.$

---

