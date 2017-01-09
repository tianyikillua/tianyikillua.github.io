---
title: Méthode de trapèze
categories:
  - 数学
---

这里运用 Méthode de trapèze 数值计算一个微分方程的解，由于 Méthode de trapèze 为隐性法，所以先运用 Méthode d'Euler explicite 计算一个预测值，然后再进行修正。与 Méthode d'Euler explicite 相比，可以发现 Méthode de trapèze 计算得的近似值与精确值更吻合。

``` matlab
function [t,y]=trapeze(y0,T,N,f)
  // ***** 程序说明 *****
  // 数值计算微分方程y'=f(t,y(t)), 初始条件t0=0, y(t0)=y0
  // 计算区间[t0,T], 即[0,T]
  // 将区间[0,T]分为N个子区间, 有t0=0, tN=T
  // 输出时间序列t, 计算得微分方程解y
  // ***** 程序开始 *****
  h=T/N; // 步长
  t=0:h:T; // 提供计算点
  y(1)=y0; // 定义初始值
  for i=1:N // 开始计算
    y(i+1)=y(i)+h*f(t(i),y(i)); // 预测值
    y(i+1)=y(i)+h/2*(f(t(i),y(i))+f(t(i+1),y(i+1))); // 利用梯形公式进行修正
  end
endfunction
    
// 试验, 设y'(t)=-λt
y0=1; // 提供初始值
T=5; // 提供计算区间
N=20; // 提供区间划分数
lambda=1; // λ=1
function ydot=f(t,y) // 提供函数f
  ydot=-lambda*y;
endfunction
// 调用 trapeze 函数进行计算
[t,y]=trapeze(y0,T,N,f);
// 与精确值进行比较
plot(t,y,'--',t,y0*exp(-lambda*t));
legend(['Trapèze';'Exact']);
```

可以发现在同样的步长 $$N=20$$ 下，相比 Méthode d'Euler explicite 方法，Méthode de trapèze 方法产生的误差已经非常小了。