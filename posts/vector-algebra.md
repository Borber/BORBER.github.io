---
title: 'Vector Algebra'
date: 2019-06-18 15:51:00
tags: [高数,学习]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/06/18/243.jpg
---

大一复习计划$(1/\infty)$

<!-- more -->

# 向量代数与空间解析几何

------



## 第一节 向量及其线性运算

1.  ### 卦限: 

    同 二维的象限 当 z 为正时 在 1 - 4 象限,反之则在 5 - 8 象限.

2.  ### 方向角与方向余弦:

    ​		$(\cos \alpha,\cos\beta,\cos\gamma) = \left (\frac{x}{|\vec r|},\frac{y}{|\vec r|},\frac{z}{|\vec r|}\right) = \frac{1}{|\vec r|}(x,y,z) = \frac{r}{\vec r} = \vec e$

    其中 $\cos \alpha,\cos\beta,\cos\gamma$ 为向量 $\vec r$ 的方向余弦,请记住这个,在后面的知识中,会用到..

## 第二节 数量级 向量积

1.  ### 数量积(点乘):

    $\vec a \bullet \vec b = |\vec a||\vec b|\cos{(\widehat{\vec a, \vec b})}$

    以此衍生出的求角度,求余弦

2.  ### 向量积(叉乘):

    $\vec a \times \vec b =|\vec a||\vec b|\sin\Theta = \begin{vmatrix}\vec i&\vec j&\vec k\\a_x&a_y&a_z\\b_x&b_y&b_z\end{vmatrix}$

    从中我们不难看出 向量积 就是 由两向量组成的平行四边形的面积 以及其方向与两向量所确定的平面垂直,这就引出了第三个话题,对点乘和叉乘的结合.

3.  ## 混合积:

    $[\vec a\vec b\vec c] = (\vec a \times \vec b)\bullet\vec c = |\vec a \times\vec b||\vec c|\cos \alpha$

    由1,2 我们不难看出,只有 $\vec a,\vec b,\vec c$ 三个向量不共面时 混合积的值才不为零,而这样一个公式,同时也提供了对平行六面体的体积的新求法.只要知道三个向量,就可以通过其中任意两个的叉乘积作为数值等于底面积的向量,与第三个向量点乘,得出体积.同时这也是一个检测三个向量是否共面的公式,还有检测三个向量能否作为三维空间的基底.

## 第三节 平面及其方程

1.  ### 点法式

    $A(x-x_0)+B(y-y_0)+C(z-z_0)=0$

    用点法式解题时,如果只给出三个点,就先找两个向量,然后使用叉乘得到一个法向量,最后使用法向量和其中一个向量组成点法式.

2.  ### 一般式 (简单 看一眼就会)

3.  ### 两平面的夹角

    通常是锐角或者直角,所以余弦值是正数,所以直接求法向量的夹角的余弦值的绝对值即是两平面的夹角的余弦值.

## 第四节 空间直线及其方程

1.  ### 空间直线在某平面的投影直线方程的求法

    -   由两个空间曲面方程确定的曲线可以直接设其中一个平面方程的$\lambda$ 倍 然后 两个平面相加 计算与所求平面相垂直的平面,求出之后,与其中平面联立 求出直线方程.  <mark oncopy=" ">详细参见 高等数学下</mark>  $P_{35} E_7$
    -   并推测 当空间直线的方程是由一般方程确立的 则直接找交点 再从直线找一点,找一条直线垂直平面 两点确定一条直线

## 第五节 曲面及其方程

## 第六节 空间曲线及其方程

1.  球面  $\begin{cases}
     x=a\sin\psi\cos\theta \\
     y=a\sin\psi\sin\theta \\ 
    z=a\cos\psi
     \end{cases}$  