---
title: 'Re-integration'
date: 2019-06-29 16:50:16
tags: [高数,学习]
published: true
hideInList: false
feature: https://www.z4a.net/images/2019/06/29/Nora-Wallpaper.jpg
---
  大一复习计划$(3/\infty)$

<!-- more -->

# 第十章 重积分

------

## 第一,二节 二重积分 及其计算

1.  $\iint_D f(x,y)d\sigma=\lim_{\lambda \to 0}{\sum_{i=1}^n{f(\xi_i,\eta_i)\Delta\sigma_i}}$ 

    1.  利用直角坐标计算二重积分

        $\iint_D f(x,y)d x d y$ 其中 $d x d y$ 叫做 直角坐标中的面积元素

    2.  利用极坐标计算二重积分

        $\iint_D f(x,y)d \sigma=\lim_(\lambda \to 0)\sum_{i=1}^n f(\xi_i,\eta_i)d \sigma_i=\iint_D f(\rho\cos\theta,\rho\sin\theta)\rho d\rho d \theta$ <mark oncopy=" ">注意</mark>   多了一个 $\rho$  

## 第三节 三重积分

1.  $\iiint_\Omega f(x,y,z)d v=\lim_(\lambda \to0)\sum_{i=1}^n f(\xi_i,\eta_i,\zeta_i)\Delta v_i$

    1.  直角坐标中的体积元素

        $\iiint_\Omega f(x,y,z)dxdydz$ 

    2.  柱面坐标计算三重积分

        $\begin{cases}
        x=\rho\cos\theta,\\
        y=\rho\sin\theta,\\
        z=z
        \end{cases}$

        $\iiint_\Omega f(x,y,z)=\iiint_\Omega F(\rho,\theta,z)\rho d\rho d\theta dz$ 

         <mark oncopy=" ">注意</mark>   多了一个 $\rho$  

    3.  球面坐标计算三重积分

        $\begin{cases}
        x=r\sin\varphi\cos\theta\\
        y=r\cos\varphi\sin\theta\\
        z=r\cos\varphi
        \end{cases}$ 

        $\iiint_\Omega f(x,y,z)=\iiint_\Omega F(r,\varphi,\theta)r^2\sin\theta dr d\varphi d\theta$ 

## 第四节 重积分的应用

1.  曲面的面积

    

    $A=\iint_D\sqrt{1+\left(\frac{\partial z}{\partial x}\right)^2+\left(\frac{\partial z}{\partial y}\right)^2} dxdy$   

2.  质心

    $\bar{x}=\frac{\iint_D x\mu(x,y)d \sigma}{\iint_D \mu(x,y)d \sigma} \\ \bar{y}=\frac{\iint_D y\mu(x,y)d \sigma}{\iint_D \mu(x,y)d \sigma}$ 

    

3.  转动惯量

    

    $I_x=\iint_D y^2\mu(x,y)d\sigma,I_y=\iint_D x^2\mu(x,y)d\sigma$  

    若是在三维坐标系中

    $I_x=\iiint_\Omega(y^2+z^2)\rho(x,y,z)dv \\I_y=\iiint_\Omega(x^2+z^2)\rho(x,y,z)dv \\I_z=\iiint_\Omega(x^2+y^2)\rho(x,y,z)dv \\$  

4.  引力

    肯定不考 不学

    

    