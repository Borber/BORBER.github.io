---
title: 'Multivariable calculus'
date: 2019-06-24 22:29:38
tags: [高数,学习]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/06/24/hometown.jpg
---
大一复习计划$(2/\infty)$


<!-- more -->


# 第九章　多元函数微分法及其应用

---


## 第一节　多元函数的基本概念

1.  当　$f(x)$  在０点无定义时，应该将$y=kx$ 带入式子判断　$k$ 　对极限的影响，而如果极限与　$k$　有关时，极限不存在

## 第二节　偏导数

1.  $\frac{\partial z}{\partial x}=f_x(x,y)\ \ \frac{\partial z}{\partial y}=f_y(x,y)$  
2.  混合偏导　对求导顺序无要求　(在区域Ｄ中连续)

## 第三节　全微分

$\lim_{(\partial x,\partial y \to (0,0))}f(x+\partial x,y+\partial y)=\lim_{\rho \to 0}[f(x,y)+\partial z]=f(x,y)$

#### 全微分在近似运算中的应用

$f(x+\partial x,y+\partial y) \approx f(x,y)+f_x(x,y)\partial x +f_y(x,y)\partial y$ 

## 第四节 多元复合函数的求导法则

![](https://www.z4a.net/images/2019/06/20/fxy.jpg)

$令 z= f(u,v);\\ f_x(u,v)=\frac{\partial z}{\partial u}\frac{\partial u}{\partial x}\\f_y(u,v)=\frac{\partial z}{\partial u}\frac{\partial u}{\partial y}+\frac{\partial z}{\partial v}\frac{d v}{d y}$ 

 <mark oncopy=" ">求到底  加起来</mark>

切记  如果 是有多个变量 则使用 $\partial \ (x)$ 如果只有一个变量 则使用 $d\ (y)$

## 第五节 隐函数求导

1.  一般形式

    $\frac{d y}{d x}=-\frac{F_x}{F_y}$

    推导流程

    $F(x,f(x))=0\\$

    全导数: 

    $\frac{\partial F}{\partial x}+\frac{\partial F}{\partial y}\frac{d y}{d x}=0\\
    \ \frac{d y}{d x}=-\frac{F_x}{F_y}$  

2.  $\begin{cases}F(x,y,u.v)=0\\G(x,y,u,v)=0 \end{cases}$

    1.  雅克比行列式:

        $J=\frac{\partial(F,G)}{\partial(u.v)}=\begin{vmatrix}\frac{\partial F}{\partial u} & \frac{\partial F}{\partial v}\\\frac{\partial G}{\partial u} &\frac{\partial G}{\partial v}\end{vmatrix}$ 

        记住就好

        

        $\frac{\partial u}{\partial x}=-\frac{1}{J}\frac{\partial(F,G)}{\partial(x,v)}=-\frac{\begin{vmatrix}F_x & F_v \\G_x & G_v\end{vmatrix}}{\begin{vmatrix}F_u & F_v \\G_u & G_v\end{vmatrix}}\\\\\frac{\partial v}{\partial x}=-\frac{1}{J} \frac{\partial(F,G)}{\partial(u,x)}=-\frac{\begin{vmatrix}F_u & F_x \\G_u & G_x\end{vmatrix}}{\begin{vmatrix}F_u &F_v \\G_u & G_v\end{vmatrix}}\\  \\\frac{\partial v}{\partial x}=-\frac{1}{J}\frac{\partial(F,G)}{\partial(y,v)}=-\frac{
        \begin{vmatrix}F_y & F_v \\G_y &G_v\end{vmatrix}}{\begin{vmatrix}F_u & F_v \\G_u & G_v\end{vmatrix}}\\  \\\frac{\partial v}{\partial x}=-\frac{1}{J} \frac{\partial(F,G)}{\partial(u,y)}=-\frac{\begin{vmatrix}F_u & F_y \\G_u & G_y\end{vmatrix}}{\begin{vmatrix}F_u &F_v \\G_u & G_v\end{vmatrix}}$ 

    上面的式子  总结成一句话 就是 你要求谁对谁的导数就把 雅克比行列式中的 对应元素 替换掉即可

    ## 第六节 多元函数微分几何学

    1.  导向量: $\lim_{t \to t_0}\frac{\Delta r}{\Delta t}=\lim_{\Delta t \to 0}\frac{f(t_0+\Delta t)-f(t_0)}{\Delta t}$ 

        在对曲线的积分中 导向量 就是 切向量,比之长度 就是单位切向量.

    2.  空间曲线的切线和法平面

         <mark oncopy=" ">参数方程形式1:</mark>

        $\begin{cases}
        x=\varphi (t) \\
        y=\psi(t) \ \ \  t\in[\alpha,\beta] \\
        z=\omega(t) \\
        \end{cases}$ 

        由导向量可知 $r=f'(t_0)=(\varphi' (t_0),\psi'(t_0),\omega'(t_0))$ 

        对应的切线方程就是:

        $\frac{x-x_0}{\varphi'(t_0)}=\frac{y-y_0}{\psi'(t_0)}=\frac{z-z_0}{\varphi'(t_0)}$ 

        对应的法平面方程是:

        $\varphi'(t_0)(x-x_0)+\psi'(t_0)(y-y_0)+\omega'(t_0)(z-z_0)=0$ 

         <mark oncopy=" ">参数方程形式2:</mark>

        $\begin{cases}
        y=\varphi (x) \\
        z=\psi(x)
        \end{cases}$

        可以转化为 :

        $\begin{cases}
        x= x\\
        y=\varphi (x) \\
        z=\psi(x)
        \end{cases}$ 

        由形式一可得:

        对应的切线方程就是:

        $\frac{x-x_0}{1}=\frac{y-y_0}{\varphi'(x_0)}=\frac{z-z_0}{\psi'(x_0)}$ 

        对应的法平面方程是:

        $(x-x_0)+\varphi'(x_0)(y-y_0)+\psi'(x_0)(z-z_0)=0$ 

         <mark oncopy=" ">参数方程形式3:</mark> 

        $\begin{cases}
        F(x,y,z)=0 \\
        G(x,y,z)=0
        \end{cases}$ 

        
        不会 打赌不考

    3.  曲面的切平面 和法线

        $F(x,y,z)=0$  

         <mark oncopy=" ">参数方程形式1:</mark>

        $(F_x(x,y,z),F_y(x,y,z),F_z(x,y,z))$ 是它的法向量  相应的:

        它的 切平面是 

        $F_x(x_0,y_0,z_0)(x-x_0)+F_y(x_0,y_0,z_0)(y-y_0)+F_z(x_0,y_0,z_0)(z-z_0)=0$

         法线方程是:

        $\frac{x-x_0}{F_x(x_0,y_0,z_0)}=\frac{y-y_0}{F_y(x_0,y_0,z_0)}=\frac{z-z_0}{F_z(x_0,y_0,z_0)}$  

        

         <mark oncopy=" ">参数方程形式2:</mark>

        $z=f(x,y)\\
        F(x,y,z)=f(x,y)-z\\
        \\
        $   

        所以 切平面方程是:

        $f_x(x_0,y_0)(x-x_0)+f_y(x_0,y_0)(y-y_0)-(z-z_0)=0$

        法线方程是:

        $\frac{x-x_0}{f_x(x_0,y_0)}=\frac{y-y_0}{f_y(x_0,y_0)}=\frac{z-z_0}{-1}$ 

        规定 法向量的方向是向上的 所以 用 $\alpha ,\beta,\gamma$ 来表示法向量的方向角

        $\alpha=-\frac{f_x}{\sqrt{1+f_x^2+f_y^2}},\beta=-\frac{f_y}{\sqrt{1+f_x^2+f_y^2}},\gamma=\frac{1}{\sqrt{1+f_x^2+f_y^2}}$ 

        因为 $x,y与z$ 不同号 所以 $\gamma$ 为正  则 $\alpha ,\beta$ 为负.

        

        ## 第七节 方向导数与梯度

        1.  方向

            设 $\alpha,\beta,\gamma$ 分别为 方向 $l$ 与 $x,y,z$ 轴的夹角.

            方向向量:

            $\boldsymbol{e}=(\cos\alpha,\cos\beta,\cos\gamma)$ 

            方向导数:

            $\left.\frac{\partial f}{\partial l}\right|_{(x_0.y_0.z_0)}=f_x(x_0,y_0,z_0)\cos\alpha+f_y(x_0,y_0,z_0)\cos\beta+f_z(x_0,y_0,z_0)\cos\gamma$ 

            算就对了

        2.  梯度

            $\boldsymbol{grad}\ f(x_0,y_0)=\nabla f(x_0,y_0)=f_x(x_0,y_0)\boldsymbol{i}+f_y(x_0,y_0)\boldsymbol{j}$

            

            $\nabla f(x_0,y_0)$  为 Nabla 算子.     

            $\left.\frac{\partial f}{\partial l}\right|_{(x_0.y_0.z_0)}=\nabla f(x_0,y_0,z_0)\bullet\boldsymbol{e}=f_x(x_0,y_0,z_0)\cos\alpha+f_y(x_0,y_0,z_0)\cos\beta+f_z(x_0,y_0,z_0)\cos\gamma$ 

        ## 第八节 多元函数的极值及其求法

        1.  多元函数极值 及 最大值 最小值

            1.  先求一阶导 确定一切驻点

                对于二元函数:

                $f_z(x_0,y_0)=0,f_y(x_o,y_0)=0$

            2.  令 $f_{x x}(x_0,y_0)=A,f_{x y}(x_0,y_0)=B,f_{y y}(x_0,y_0)=C$ 当:

                (1)$A C-B^2 \gt 0$ 

                1.  $A \lt 0$  时 有极大值
                2.  $A \gt 0$  时 有极小值

                (2)$A C-B^2 \lt 0$ 没有极值

                (3)$A C-B^2 =0$ 可能有 可能没有 另作讨论

        2.  条件极值 拉格朗日乘数法

            1.  找条件 $\varphi$
            2.  $\begin{cases}
                f_x(x,y)+\lambda\varphi_x(x,y)=0\\
                f_y(x,y)+\lambda\varphi_y(x,y)=0\\
                \varphi(x,y)=0 \\
                \end{cases}$  
            3.  求 $\lambda$ 