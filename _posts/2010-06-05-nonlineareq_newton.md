---
title: Méthode de Newton
categories:
  - 数学
---

下面来讲讲牛顿迭代法，牛顿迭代法也是不动点法 (Méthode de point fixe) 的一个例子，即要求...

$$
f(x)=0
$$

我们将方程写为等同形式...

$$
x_{i+1}=g(x_i)
$$

然后对它不断迭代，如果收敛，那么就求得了一个解。牛顿迭代法的 $$g(x)$$ 为...

$$
g(x)=x-\frac{f(x)}{f'(x)}
$$

即有...

$$
x_{i+1}=x_{i}-\frac{f(x_{i})}{f'(x_{i})}
$$

在 Scilab 中，我们可以直接写为 

$$
x=x-\frac{f(x)}{f'(x)}
$$

只需一次次执行命令即可一次次对 $$x$$ 进行迭代。若 $$f:\mathbb{R}^n\to\mathbb{R}^n$$，即 $$f$$ 是一个多元函数，那么有...

$$
x_{i+1}=x_{i}-J_f^{-1}(x_i)f(x_i)
$$

下面给出的 Scilab 代码可以运用牛顿迭代法进行求解方程 $$f(x)=0$$。

``` matlab
function x=newton(x0,f,J,eps)
  // 数值计算f(x)=0的一个解, 无论f是多元函数还是一元函数均可使用
  // 如需要解 x1+sin(x2)=0, tan(x1)+cos(x2)=5
  // 那么可以这样定义函数f
  // function y=f(x)
  //   y=[x(1)+sin(x(2));tan(x(1))+cos(x(2))-5];
  // endfunction
  // 就将问题转变为标准形式, 即求f(x)=0的一个解
  // ***** 程序说明 *****
  // 初始值为x0, 多元函数时x0为一列向量, 如x0=[1;2]
  // J为函数f的雅可比矩阵, 一元函数时J即为f的导函数
  // eps为计算精度
  // 输出为满足f(x)=0的一个接近x0的近似解, 多元函数时为一列向量, 如x=[0;1]
  // ***** 程序开始 *****
  x=x0; // 初始值
  while norm(f(x))>eps // 由于要求f(x)=0, 所以当f(x)绝对值大于某一精度时要继续迭代
    x=x-J(x)\f(x);
    // 第18行说明如下
    // 若f为一元函数, 则牛顿法迭代为
    // x=x-f(x)/f'(x)=x-f(x)/J(x)=x-J(x)\f(x) 注意"\"的含义
    // 若f为多元函数, 则牛顿法迭代为
    // x=x-inv(J(x))*f(x), 其中inv(J(x))为雅可比矩阵J(x)的逆
    // Scilab中, 计算inv(A)*b最好的方法是用"\"
    // 即 x=x-J(x)\f(x)
    // T_T 整个函数其实关键就一行呀
  end
endfunction
    
// 试验一, 解x^2-x=1
x0=1; // 提供初始值
function y=f1(x) // 提供函数f1
  y=x^2-x-1;
endfunction
function y=J1(x) // 提供函数J1
  y=2*x-1;
endfunction
eps=1e-6; // 提供精度
x=newton(x0,f1,J1,eps);
disp(x);
    
// 试验二,解
// x^2-y=0
// (x-1)^2+(y-6)^2=25
// 可以将变量x与y分别设为x1, x2, 即一个矢量的两个分量
x0=[2;2]; // 提供初始值
function y=f2(x) // 提供函数f2
  y=[x(1)^2-x(2);(x(1)-1)^2+(x(2)-6)^2-25]; // 输出也为一个两行的列向量
endfunction
function y=J2(x) // 提供函数J2
  y=[2*x(1) -1;2*(x(1)-1) 2*(x(2)-6)] // 输出为一个2乘2的矩阵
endfunction
eps=1e-6;
x=newton(x0,f2,J2,eps);
disp(x);
```

对于试验一，运行后可以得到： 

$$
x=1.618034
$$

而试验二，有 

$$
\mathbf{x}=\begin{bmatrix}1\\1\end{bmatrix}
$$
