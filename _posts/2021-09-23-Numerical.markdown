---
layout: post
title:  "Numerical Analysis Hw1"
date:   2021-09-23 21:03:36 +0530
categories: Mathematics Numerical_Analysis
published: true
use_math: true
---



### Problem 1

- Use each of the following methods to find a solution in $[0.1, 1.0]$ accurate to within $10^{-4}$ for

$600x^4 − 550x^3 + 200x^2 − 20x − 1 = 0$

First, the real root is $x≈0.232353$

**(a) Bisection Method**

This algorithm is the root-find-algorithm which dividing the section where the root must exist 

This algorithm works by the following process.

step 1:    set $p_n = \frac 1 2 (a_n + b_n )$

step 2:    $|b_n - a_n| <\epsilon $ 
then return $p_n$

step 3:    if $f(b) f(c)< 0$ then $( a_{n+1}  , b_{n+1} ) = (p_n,b_n)$  Else, $(a_{n+1} , b_{n+1} ) = (a_n , p_n)$

step 4:    go back to step $1$

Then, $\left\vert a_{n+1} - b_{n+1} \right\vert < \frac 1 2 \left\vert a_n - b_n\right\vert < \frac 1 {2^n} \left\vert a_1 - b_1\right\vert $ . 

Set $a_1 = 0.1 , b_1 = 1.0$ , $\epsilon = 10^{-4}$ , 

it is enough to iteration $n > -\log_2 \frac {10^{-4}} {\left\vert 1.0 - 0.1\right\vert } >13$ times.

And use above algorithm, we get $0.232330$ as solution by 14 step

```python
n =  0 	 a=0.100000 , b=1.000000
n =  1 	 a=0.100000 , b=0.550000
n =  2 	 a=0.100000 , b=0.325000
					...
n = 12 	 a=0.232275 , b=0.232495
n = 13 	 a=0.232275 , b=0.232385
n = 14 	 a=0.232330 , b=0.232385
result : 0.232330
```

Execution Result of “pb1-a_bisection.py”

**(b) Secant method**

This algorithm is the root-find-algorithm which use secant line.

This algorithm works by the following process.

step 1:    $x_{n+1} = x_n - f( x_n )  \frac { x_n - x_{n-1}} {f(x_n) - f(x_{n-1})}$

step 2:    if $\left\vert f(x_{n+1})\right\vert < \epsilon$ then return $x_{n+1}$

step 3:    go back to step 1

Set $x_0 = 0.1 , x_1 = 1.0$, $\epsilon = 10^{-4}$ and use above algorithm, we get 0.232353 by 6 steps

```python
n =  0 	 a=0.100000 , b=1.000000
n =  1 	 a=1.000000 , b=0.105818
n =  2 	 a=0.105818 , b=0.111457
n =  3 	 a=0.111457 , b=0.311777
n =  4 	 a=0.311777 , b=0.219541
n =  5 	 a=0.219541 , b=0.231352
n =  6 	 a=0.231352 , b=0.232363
result : 0.232353
```

Execution Result of “pb1-b_secant.py”

**(c) Newton’s method**

This algorithm is the root-find-algorithm which use tangent line

This algorithm works by the following process.

step 1:    $x_{n+1} = x_n - \frac {f( x_n )} {f'(x_ n )}$ 

step 2:    if $\left\vert f(x_{n+1})\right\vert < \epsilon$ then return $x_{n+1}$

step 3:    go back to step 1

Set $x_1 = 0.1$, $\epsilon = 10^{-4}$ and use above algorithm, we get 0.232353 by 4 steps

```python
n =  0 	 x=0.100000
n =  1 	 x=0.352542
n =  2 	 x=0.258921
n =  3 	 x=0.232964
n =  4 	 x=0.232353
0.232353
```

Execution Result of “pb1-c_Newton.py”

### Problem 2

- For the same initial approximation x0, estimate the rate of convergence for each method
in the problem 1

If there exist real number $\lambda >0$ and $\alpha \geq 1$ such that

$
\lim \limits_{n \rightarrow \infty} \frac {|x _ {n+1} - r |} {|x_n - r|^{\alpha}} = \lambda 
$

then we say that $α$ is the rate of convergence of the sequence. [2]

The rate of convergence for each method is as follows.[3][4][5]

$$
 \begin{align*}&\alpha_{bisection} =1 \\&\alpha_{secant} = \frac{1 + \sqrt 5} 2 \approx 1.618\\ &\alpha_{newton} = 2  \end{align*} 
$$

Following the formula (9) in rate.pdf , $\alpha$ and $x_n$ are hold follow.

$
\alpha \approx \frac {\log |(x_{n+1} - x_n )/ (x_n - x_{n-1})|}{\log|(x_n - x_{n-1}) / (x_{n-1} - x_{n-2})|}
$

Let’s apply it in those three methods.

Put the $x_n$ values in the “List” variable and print approximate values $\alpha$ by using below script.

Since $n \rightarrow \infty$ then approximate value $\alpha$ goes to real rate of converge each method, so we select n as big as possible.

```python
from math import log

def alpha(a,n ):
    return log(abs ((a[n+1] - a[n]) / (a[n] - a[n-1]))) / \
						 log(abs ((a[n] - a[n-1]) / (a[n-1] - a[n-2]))) 

print("%.4f"%alpha(List , len(a)-2))
```

Then we can get follow result as approximate values.

```python
bisection	:  	0.9740
secant 	  : 	1.8704
newton 	  : 	2.0721
```

Execution Result of “pb2-estimate.py”

It is very close values from theorical values of each rate of converge.

### Problem 3

- $f(x) = 10x^3 −8.3x^2 + 2.295x−0.21141 = 0$  has a root at $x = 0.29$. Use Newton’s method with an initial approximation $x_0 = 0.28$ to find this root. Explain what happens.

When the initial value is $0.28$ and apply Newton’s method for accuracy $10^{-10}$, then root value converge to $0.27$, not known root $0.29$.

```python
0 	 0.280000
1 	 0.270000
0.270000
```

Execution Result of “pb3_0.28.py”

But, when initial value is $0.30$ and apply Newton’s method, then we can get $0.29$ what we want.

```python
0 	 0.300000
1 	 0.294000
2 	 0.291000
3 	 0.290087
4 	 0.290001
5 	 0.290000
0.290000
```

Execution Result of “pb3_0.30.py”

So, we can conclude that Newton’s method give us difference solution following the initial value when there is more than one solutions.

In fact, 0.27 is not a root to the equation.  But it is difficult to distinguish numerically because other two root not a 0.29 are have 0.27 as real part, and the imaginary part is very small, about $10^{-8}$  [6].

### Problem 4

- Steffensen’s method 
Suppose that $x = g(x)$ has the solution p with $g(p) \neq 1$. 
If there exists a $δ > 0$ such that $g ∈ C^3[p − δ, p + δ]$. 
Prove the Steffensen’s method gives quadratic convergence for any $p_0 ∈ [p − δ, p + δ]$

Steffensen’s method is operated through the following process.[7]

To find a solution $p = g(p)$ , given an initial value $p_0$

step 1:    $x_n = g(p_n)$

step 2:    $y_n = g(x_n )$

step 3:    $p_{n+1} = p_n - \frac {(x_n - y_n)^2} {y_n - 2x_n + p_n}$

step 4:    if $\left\vert p_{n+1} - p_n\right\vert < \epsilon$ , return $p_{n+1}$

step 5:    go back to step 1

So, we can get recurrence relation ****for steffensen’s method as follow;

$
p_{n+1} = p_n - \frac {(g(p_n) - p_n )^2} {g(g( p_n) ) - 2 g(p_n ) + p_n}
$

Let’s $f(x) := g(x) - x$  then problem become to find $p$ such that $f(p) = 0$.

So,

$$
\begin{align*} g(g( p_n) ) - 2 g(p_n ) + p_n &= (g( g(p_n)) - g(p_n)  ) - (g(p_n) - p_n)\\&=f(g(p_n)) - f(p_n) \\&=f(p_n + f(p_n)) - f(p_n)\end{align*} 
$$

and we get follow

$
p_{n+1} = p_n - \frac {(f(p_n))^2} {f(p_n + f(p_n)) - f(p_n)}
$

Set $F(x) := x -\frac {(f(x))^2} {f(x + f(x)) - f(x)}$ then its method is represent by $p_{n+1} = F(p_n )$.

From $g \in C^3[p - \delta , p+ \delta]$ , we can get also $f,F \in C^3[p - \delta , p+ \delta]$.

Set $p_0 \in [p - \delta , p+\delta]$

Since $F(x)  = x- f(x) / \frac {f(x)} {f(x + f(x)) - f(x)}$  and $f^\prime(p) = g ^\prime(p) -1 \neq 0$, we get follow;

$
\lim \limits _{x \rightarrow p} F(x) = p- \frac {f(p)} {f^\prime (p)}  = p
$

Then, $F(p) = p$.

By Taylor's theorem, 

$
f(x+f(x))= f(x) + f^{\prime}(x)f(x) + (f(x))^2 f^{\prime \prime} (\xi_1  )
$

for some $\xi_1$ which in between $x$ and $f(x)$ , and

$$
\begin{align*}F(x) &= x- \frac {(f(x))^2} {f^{\prime}(x)f(x) + (f(x))^2 f^{\prime \prime} (\xi_1  )}\\&= x - \frac {f(x)}{f^{\prime} (x) + f(x) f^{\prime \prime} (\xi_1  )}\end{align*}
$$

From $F(p) = p$ and $f(p) = p$ , we get 

$$
\begin{align*} F(x) - F(p) = x - p - (f(x) - f(p)) \frac 1 {f'(x) + f(x) f^{\prime \prime} (\xi_1  )} \end{align*}
$$

Note that $\lim \limits _{x \rightarrow p} f^{\prime \prime}( \xi_1 ) = 0$. Then we have follow

$$
\begin {align*}  F'(p) &= \lim \limits_{x \rightarrow p } \frac {F{(x)} - F(p)}{x-p} \\&= \lim \limits_{x \rightarrow p } \left( 1 - \frac {f(x)  -f (p)} { x- p }  \frac 1 {f^{\prime} (x) + f(x) f^{\prime \prime} (\xi_1 )} \right) \\&=1 - f^{\prime} (p) \frac 1 {f^{\prime }(p)} = 0\end{align*}
$$

Therefore, $F^{\prime}(p) = 0$

Let’s $e_n := p_n  - p$. 

By Taylor's theorem, we get follow;

$$
\begin{align*} p_{n+1} &=F(p_n )\\ &= F(p + e_n )\\&=p_n + e_n F^\prime (p) +  {e_n} ^2 \frac 1 2 F^{\prime \prime} (p) + {e_n}^3  F^{\prime\prime\prime}(\xi_2) \end{align*}
$$

for some $\xi_2$ which in between $p$ and $p_n$.

Therefore, we have 

$
e_{n+1} = e_n F^{\prime} (p) + {e_n}^2 \frac 1 2 F^{\prime\prime} (p) + {e_n}^3  F^{\prime\prime\prime}(\xi_2)
$

Since $F^{\prime}(p) = 0$, we have $e_{n+1} =  {e_n}^2 \frac 1 2 F^{\prime\prime} (p) + {e_n}^3 F^{\prime\prime\prime}(\xi_2)$ 

If $\delta <1$ then $0 \leq \left\vert e_{n+1} \right\vert \leq  {e_n}^2$ so $e_n$ can be converge to 0 for proper $\delta$.

For that $\delta$, 

$$
\begin{align*}\lim \limits _{n \rightarrow \infty}\frac {|p _{n+1} - p |}{|p_n - p|^2} &= \lim \limits _{n \rightarrow \infty} \frac {|e_{n+1}|}{|e_n|^2} \\&= \lim \limits _{n \rightarrow \infty}\frac 1 2 F^{\prime \prime} (p) + e_n F^{\prime \prime \prime} (\xi _2)\\&= \frac 1 2 F^{\prime \prime} (p) < \infty\end{align*}
$$

So, the rate of converge is 2.

Since $p_0$ is arbitrary , it hold for any $p_0 ∈ [p − δ, p + δ]$ for proper $\delta$

- Use the Steffensen’s method to approximate the solutions of the following equations to within$10^{−5}$ and discuss the rate of convergence compared with the regular fixed point iteration
method with the same initial points

$
x = (2 − e^
x + x^
2
)/3
$

Assume that $g$ is differentiable, $p_{n+1} = g(p_n )$ converge, 

then for $e_n = p_{n} - p$ , we have $e_n \rightarrow 0$ as $n \rightarrow \infty$.

And we use Taylor’s theorem then we  can get follow;

$$
\begin{align*}p_{n+1} &= g(p_n) \\&=g(p + e_n) \\&= g(p) + e_n g'(p) + {e_n}^2 \frac 1 2 g''(\xi_3)\\&= p + e_n g'(p) + {e_n}^2 \frac 1 2 g''(\xi_3)\end{align*}
$$

for some $\xi_3$ which in between $p$ and $p_n$

So,

$
e_{n+1} =e_n g'(p) + {e_n}^2 \frac 1 2 g''(\xi_3 )
$

and we have

$$\begin{align*}\lim \limits _{n \rightarrow \infty} \frac {|p_{n+1} - p|} {|p_n - p|} &= \lim \limits _{n \rightarrow \infty} \frac {e_{n+1}} {e_n} \\&=\lim \limits _{n \rightarrow \infty}  (g'(p) + e_n \frac 1 2 g''(\xi_3 ))\\&=g'(p) < \infty \end{align*}$$

Therefore, fixed point iteration method converge **linearly,** 

So, fixed point iteration method converge  theoretically slower than steffensen’s method.

So, we expect that the each estimate values of rate of converge is 2 for steffensen, and 1 for fixed point.

Follow is the result for initail point is $-1$ within $10^{-5}$

```python
initial point : -1  , acc = 1e-05

root by steffensen :  0.25753028543986073
total step :  4
rate of converge 2.244690

root by fixed_iter :  0.25752734154531925
total step :  10
rate of converge 1.000203
```

Execution Result of “pb4.py”

We can see that the results are calculated similarly to 1 and 2, like theoretical rates.

Also, we can see that the steffensen’s method has a small number of steps performed to find the root.

### Problem 5

- Find approximations to within $10^{−5}$ to all the zeros of the following problems by
the first finding the real zeros using Newton’s method and then reducing to polynomials of lower degree to determine any complex zeros by using the Muller’s method (section 2.6)
a. $f(x) = x^4 − 2x^3 − 4x^2 + 4x + 4$
b. $f(x) = x^4 − 2x^3 − 12x^2 + 16x − 40$

The algorithm is similar to the Newton’s method, but the difference thing is that it does not require derivatives.

This algorithm works by the following process.

step 1:

$
h_{n-1} = p_{n-1} - p_{n-2}
$

$h_{n} = p_{n} - p_{n-1}$

$
\delta_{n-1} = \frac {f(p_{n-1}) - f(p_{n-2})} {p_{n-1} - p_{n-2}}$ 


$\delta_n =\frac {f(p_n) - f(p_{n-1})} {p_n - p_{n-1}} $


$
d_n = \frac {\delta_n - \delta_{n-1}} {h_{n-1} + h_n}
$


step 2:


$b_n = \delta_n + h_n d_n$ 


$D_n = \sqrt{b_n^2 - 4f(p_n)d_n}$

step 3: 

if $\left\vert b_n-D_n \right\vert < \left\vert b_n+D_n\right\vert $ then $E = b_n+D_n$

else, $E = b_n - D_n$

step 4:

$
e_n = -2f( p_n ) / E_n \\ p_{n+1} = p_n + e_n
$

step 5:

if $e_n < \epsilon$ return $p_{n+1}$

else, go back to step 1   


To implement the educing to polynomials of lower degree, we can consider follow property

If the polynomial $P(x) , Q(x)$ hold $P(x) = (x-a)Q(x)$ , then 

$
Q(x) = \frac {P(x)} {x-a}
$

when $x \neq a$

So , we can implement it as follows.

```python
def red(f, x, roots):
    if len(roots) == 1:
        return f(x) / (x-roots[0])
    return red(f, x , roots[1:]) / (x-roots[0])
```

The follows are results using the Newton’s method and this algorithm in the above two equations

we can obtain the first root by Newton's method, and then the remaining three roots by iterating the Miller method.

```python
the all roots of equation a 
3.0286332070637134
(0.423522-0.72440523j)
(0.423522+0.72440523j)
(-1.87567721+0j)

the all roots of equation b 
-3.54823289798023
(0.58355973+1.49418801j)
(0.58355973-1.49418801j)
(4.38111344+0j)
```

Execution Result of “pb5.py”

Therefore, 

For

$f(x) = x^4 − 2x^3 − 4x^2 + 4x + 4$

Then, its roots are follow;

$x_1 = 3.0286332070637134$

$x_2 = 0.423522-0.72440523i$

$x_3 = 0.423522+0.72440523i$

$x_4 = -1.87567721$

And, for

$f(x) = x^4 − 2x^3 − 12x^2 + 16x − 40$

Then, its roots are follow;

$x_1 = -3.54823289798023$

$x_2 = 0.58355973+1.49418801i$

$x_3 = 0.58355973-1.49418801i$

$x_4 = 4.38111344$

### Reference

[1] The root of given equation in problem 1 : https://www.wolframalpha.com/input?i=600x^+4+−+550x^+3+%2B+200x^+2+−+20x+−+1+%3D+0

[2] rate.pdf

[3] Bisection_mehod is linear from wiki : https://en.wikipedia.org/wiki/Bisection_method#Analysis

[4] convergence of secant method from wiki https://en.wikipedia.org/wiki/Secant_method#Convergence

[5] Newton mtehod is converge quadratic and its proof from wiki : https://en.wikipedia.org/wiki/Newton's_method#Proof_of_quadratic_convergence_for_Newton's_iterative_method

[6] The roots of given equation in ploblem 3 : https://www.wolframalpha.com/input?i=0%3D+10x^+3+−8.3x^+2+%2B+2.295x−0.21141+

[7] Richard L. Burden &J. Douglas Faires(,2010.) , Accelerating Convergence(10th), Numerical Analysis. (pp 88-89). Cengage Laerning

3.0286332070637134
(0.423522-0.72440523j)
(0.423522+0.72440523j)
(-1.87567721+0j)

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
