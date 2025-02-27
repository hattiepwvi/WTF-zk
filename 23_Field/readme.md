---
title: 23. 域
tags:
  - zk
  - abstract algebra
  - field theory
  - field
---

# WTF zk 教程第 23 讲：域

这一讲，我们介绍域，它是一种特殊的环，支持加减乘除运算，在各种密码协议中起着关键作用。

## 1. 域

在之前的教程中我们学了群和环，下面是域和它们的对比：

- 群：支持加法，减法（加法的逆运算）。

- 环：支持加法，减法，乘法。

- 域：支持加法，减法，乘法，除法（乘法的逆运算）。

若交换环 $(F, +, \cdot)$ 的乘法群去除零元素后 $(F-\set{0}, \cdot)$ 能形成Abel群，那么我们称 $F$ 为域。也就是说域 $(F, +, \cdot)$ 满足以下性质：

1. 集合 $R$ 和加法构成的加法群 $(F, +)$ 为Abel群。

2. 集合 $R$ 去掉零元之后和乘法构成的群 $(F-\set{0}, \cdot)$ 为Abel群。

3. 加法和乘法满足分配律：即对于任意 $a, b, c \in R$，有

    - $a \cdot (b + c) = a \cdot b + a \cdot c$
    - $(a + b) \cdot c = a \cdot c + b \cdot c$。

也就是说，相比于交换环，域要求其中的任意元素 $a \in \set{F-\set{0}}$ 存在乘法逆元 $a^{-1}$，也可以记为 $\frac{1}{a}$。

常见的域包括有理数域 $\mathbb{Q}$，实数域 $\mathbb{R}$，整数模 $p$ 域 $Z_p$（其中 $p$ 为质数）。

整数环 $\mathbb{Z}$ 不能构成域，因为除了 $1$ 和 $-1$，其他元素在整数中都不存在逆元，比如 $2 \cdot \frac{1}{2} = 1$，但是 $\frac{1}{2}$ 不是整数。

当 $n$ 为合数时，整数模n环 $Z_n$ 不能构成域，因为与 $n$ 不互质的元素不存在逆元。比如 $Z_6$ 的元素 $2$ 和 $3$ 没有逆元，因此不能构成域。而当 $n$ 为质数时，整数模n环 $Z_n$ 构成域，比如 $Z_5$ 可以构成域。

## 2. 域的性质

域除了拥有环的所有性质之外，还有一些特别的性质。

**性质1.** 任何域 $F$ 中至少有 $2$ 个元素，即加法单位元（零元） $0$ 和乘法单位元 $1$。

<details><summary>点我展开证明👀</summary>

根据定义，域存在 $0$ 和 $1$，我们需要证明 $0 \neq 1$。如果 $0 = 1$，那么 $F - \set{0}$ 为空集，不能构成乘法群，因此 $0 \neq 1$，任何域 $F$ 中至少有 $2$ 个元素。证毕

</details>


**性质2.** 元素 $a, b$ 来自域 $F$，且 $a$ 和 $b$ 均不是零元，那么有 

$$
\frac{1}{a \cdot b} = \frac{1}{a} \cdot \frac{1}{b}
$$

<details><summary>点我展开证明👀</summary>

证明这个命题等同于证明 $a \cdot b$ 和 $\frac{1}{a} \cdot \frac{1}{b}$ 互为逆元。根据乘法交换律，$a b \frac{1}{a}  \frac{1}{b} = a \frac{1}{a} b \frac{1}{b} = 1 \cdot 1 = 1$。因此， $a \cdot b$ 和 $\frac{1}{a} \cdot \frac{1}{b}$ 互为逆元。证毕

</details>

**性质3. 域中无零因子（域是整环）** 元素 $a, b \in F$，若 $ab = 0$，那么有 $a = 0$ 或 $b = 0$。

<details><summary>点我展开证明👀</summary>

证明这个命题等同于证明 $a \cdot b$ 和 $\frac{1}{a} \cdot \frac{1}{b}$ 互为逆元。根据乘法交换律，$a b \frac{1}{a}  \frac{1}{b} = a \frac{1}{a} b \frac{1}{b} = 1 \cdot 1 = 1$。因此， $a \cdot b$ 和 $\frac{1}{a} \cdot \frac{1}{b}$ 互为逆元。证毕

</details>

**性质4. 域的特征** 若存在正整数n使得 $0 = n \cdot 1 = 1 + 1 + ... + 1 $（其中有n个1），那么这样的n中最小的一个称为这个域的**特征**。域的特征要么是一个素数 $p$，要么是 $0$（表示这样的n不存在）。

<details><summary>点我展开证明👀</summary>

假设 $n$ 为合数，那么存在 $a, b \in F$，使得 $n = ab$ 成立。根据特征的定义，有 $n \cdot 1 = 0$，也就是 $a \cdot b cdot 1 = 0$，得到 $ab = 0$。根据性质3（域中无零因子），得到 $a = 0$ 或 $b = 0$，也就是 $n = ab = 0$，与假设矛盾。因此 $n$ 不是合数。

当 $n$ 为素数 $p$ 时，特征为 $p$，比如 $Z_5$。

对于无限域，比如有理数域 $R$，特征不存在，此时 $n = 0$。

</details>

**性质5.** 一个交换环是域当且仅当它的理想只有自身和零理想。

<details><summary>点我展开证明👀</summary>

**充分性**

设 $R$ 是一个域，$I$ 是 $R$ 的理想，其中 $I$ 不等于 $\set{0}$。我们需要证明 $I = R$。

首先，我们证明域的乘法单位元 $1$ 在 $I$ 中。因为 $I \neq \set{0}$，因此存在元素 $a \in I$ 且 $a \neq 0$，它的逆元 $a^{-1}$ 存在且在域 $R$ 中。根据理想的吸收律，有 $a a^{-1} = 1 \in I$，因此 $1 \in I$。

接下来，对于任意 $b \in R$，根据吸收律，有 $1 \cdot b =b \in I$，也就是 $R \subseteq I$。根据理想的定义，有 $I \subseteq R$，因此 $I = R$。证毕。

**必要性**

设 $R$ 是一个交换环，且对于 $R$ 的每个非零理想 $I$，有 $I = R$。考虑 $R$ 中的非零元素 $a$，我们将证明存在 $a^{-1} \in R$ 使得 $a \cdot a^{-1} = a^{-1} \cdot a = 1$。

对于 $R$ 中任意元素 $a$，我们考虑由 $a$ 生成的主理想： $I = (a) = \set{ra \mid r \in R}$。由于 $I$ 不是零理想且 $I = R$。因此，存在 $b \in R$ 使得 $ab = 1$，也就是 $a^{-1} = b \in R$。因此，交换环 $R$ 中任意元素存在逆元， $R$ 是域。证毕。

</details>

## 3. 子域

对于域 $F$ 和集合 $K$，有 $K \subseteq F$，且 $K$ 与 $F$ 中的加法和乘法运算构成域，那么我们称 $K$ 为 $F$ 的**子域**，而 $F$ 为 $K$ 的**扩域**。

这个条件等价于：

1. $K \subseteq F$
2. $1_K = 1_F$
3. $K$ 中的任意元素在域 $F$ 的加法和乘法运算中封闭。
4. $K$ 中的任意元素存在加法逆元和乘法逆元。

举个例子，有理数域 $\mathbb{Q}$ 是实数域的 $\mathbb{R}$ 的子域，它们拥有相同的零元 $0$ 和乘法单位元 $1$。

举几个反例，整数不是实数域的 $\mathbb{R}$ 的子域，虽然整数是实数的子集，但是整数不能形成域；整数模2域 $Z_2$ 不是整数模5域 $Z_5$ 的子域，虽然 $Z_2 \subseteq Z_5$，但是它们的运算分别是模2和模5下的加法和乘法，而 $Z_2$ 并不能在模5加法下封闭，比如 $1+1 \equiv 2 \pmod{5} \notin Z_2$。

在之后的教程中，我们会深入学习扩域这个概念。

## 4. 总结

这一讲，我们介绍了域及其性质。域是一种特殊的环，支持加减乘除运算，很多密码学/零知识证明算法都是建立在域上的。