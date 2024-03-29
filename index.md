<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        })
    </script>
</head>





### Learning Notes for Machine Learning

**Peilin Liu**
**from 2019.11.29**

**Outline:**

<!-- TOC -->

- [Learning Notes for Machine Learning](#learning-notes-for-machine-learning)
    - [1. Random Design Analysis of Ridge Regression](#1-random-design-analysis-of-ridge-regression) 
    - [2. Non-Asymptotic Analysis of Stochastic Approximation Algorithms](#2-non-asymptotic-analysis-of-stochastic-approximation-algorithms)   
    - [3. Optimal Learning Rates for Kernel Partial Least Squares](#3-optimal-learning-rates-for-kernel-partial-least-squares)
    - [4. Non-Strongly-Convex Smooth Stochastic Approximation with Convergence Rate O(1/n)](#4-non-strongly-convex-smooth-stochastic-approximation-with-convergence-rate-o1n) 
    - [5. The Tradeoff of Large Scale Machine Learning](#5-the-tradeoff-of-large-scale-machine-learning)
<!-- /TOC -->

#### 1. Random Design Analysis of Ridge Regression

- **Abstract :** 
  <font size=3>
  
  &emsp;&emsp;传统的最小二乘方法或是其变种岭回归估计，在一般的假设情境下（即样本点的方差结构完全已知的情况下），虽然能够快速方便得出关于回归系数的估计量，但由于抽样出现的偏差，使得所得系数很可能不能很好地对于在样本外的数据点进行良好的预测，所以在这里提出了基于Random Design的参数估计方法，将对于未知数据的预测效果纳入到考量范围之中。
  
  &emsp;&emsp;文章当中主要基于简单的误差分解，研究数据点的方差结构$\hat{{\Sigma}}$，相应变量中的噪声$\sigma$，以及数据模型与线性模型的吻合程度，对于最后估计系数准确度的影响。
  
  
</font>

- **Assumptions :**
  
- **Theorems :**<font size=3>
  &emsp;&emsp;
</font>

- **Technical Skills :**
  
- **Summary :**

#### 2. Non-Asymptotic Analysis of Stochastic Approximation Algorithms

- **Abstract :**
  <font size=3>
  
  &emsp;&emsp;这篇文章主要考虑对于定义在Hilbert Space上的凸目标函数的优化，但必须通过其梯度的无偏估计实现。本篇文章的分析证实了学习率与迭代次数的倒数之间呈比例关系，并且在强凸性要求下可以在这样的学习率下达到最优的收敛速率，但这样的结果对于非强凸性的情况和比例常数的设定不鲁棒。但这样的问题可以在进行averaging（$\bar\theta_n={\frac{1}{n+1}}\sum_{i=0}^{n}\theta_{i}$）和降低下降速率（$\gamma_n=Cn^{-\alpha}$）即减小$\alpha$的情况下被解决，能够鲁棒地得到最优的收敛速率，对于不同的条件设定（强凸或者非强凸性）均具有良好的鲁棒性。
  
- **Assumptions :**
  
- **Theorems :**
  
- **Technical Skills :**
  
- **Summary :**

#### 3. Optimal Learning Rates for Kernel Partial Least Squares

- **Abstract :**

- **Assumptions :**
  
- **Theorems :**
  
- **Technical Skills :**
  
- **Summary :**

#### 4. Non-Strongly-Convex Smooth Stochastic Approximation with Convergence Rate O(1/n)

- **Abstract :**
  <font size=3>
  
  &emsp;&emsp;这篇文章主要舍弃了前人在做随机逼近时对于目标函数的强凸性假设（**Hessian阵为严格的positive definitive and invertible**，i.e. $f(\theta^\prime) \geqslant f(\theta) + \langle f^\prime(\theta),\theta^\prime - \theta \rangle + \frac{u}{2!}||\theta^\prime - \theta||^2, u>0$），而是在一般的假设条件下（例如，知道某点处梯度的无偏估计），分析了两种算法，将现有算法的收敛速率从$O(1/\sqrt{n})$提高到了$O(1/n)$：第一种算法针对于我们熟悉的least-squares regression：**averaged SGD with a constant step-size**；第二种算法针对于logistic regression：**a simple novel algorithm a)构建对于损失函数的连续局部二次逼近，b)并且使得时间复杂度与SGD相同。**
  **ps：在证明过程中，为保证连贯性，两算法的损失函数和其他设定都使用了较为一般的表达形式，e.g. $loss\ function：f(\theta) = E[l(y_n,\langle x_n, \theta\rangle)]$**

</font>
&nbsp;

- **Assumptions :**

<font size = 3>
    

  **Constant-Step-Size least-mean-squares algorithm：**
   
   A1. 解释变量（or协变量）数据所处空间为欧式空间，维度为d。
   
   A2. 每一组观测数据i.i.d.
   
   A3. 相应变量与解释变量在概率意义下均方可积. Define $H = E(x_n\otimes x_n)$
   
   A4. Define $f(\theta)=(1 / 2) \mathbb{E}\left[\left\langle\theta, x_{n}\right\rangle^{2}-2\left\langle\theta, z_{n}\right\rangle\right]$ attains the global minimum at a certain $\theta^\ast$ and the residual $\xi_{n}=z_{n}-\left\langle\theta_{*}, x_{n}\right\rangle x_{n}$
   
   A5. 参数迭代：$\theta_{n}=\theta_{n-1}-\gamma\left(\left\langle\theta_{n-1}, x_{n}\right\rangle x_{n}-z_{n}\right)=\left(I-\gamma x_{n} \otimes x_{n}\right) \theta_{n-1}+\gamma z_{n}$ start from $\theta_{0} \in \mathcal{H}$. &emsp;&emsp;**ps:将目标函数求导后所得的表达式为expected gradient，利用empirical gradient替代即为上式**
   
   A6. 残差矩阵与离差阵被Hessian($\theta^\ast$)控制：$\mathbb{E}\left[\xi_{n} \otimes \xi_{n}\right] \preccurlyeq \sigma^{2} H \text { and } \mathbb{E}\left(\left\|x_{n}\right\|^{2} x_{n} \otimes x_{n}\right) \preccurlyeq R^{2} H$
   ps: A1-A5都是随机模拟中较为常见的标准假设，对于最小二乘回归而言，$z_n = x_ny_n$

   A7. $\Arrowvert x_n \Arrowvert ^2 \le R^2 \ a.s.$，残差外积矩阵Hessian($\theta^\ast$)控制, 以及关于残差的p阶矩常数限制假设，以及关于$x_n$的投影峰度假设: $$\forall z \in \mathcal{H}, \quad \mathbb{E}\left\langle z, x_{n}\right\rangle^{4} \leqslant \kappa\langle z, H z\rangle^{2}$$

   B1. 输入空间为d维欧氏空间。

   B2. $(x_n, y_n) \in \mathcal{H} \times {\{-1,1\}}$ are i.i.d.

   B3. 下列求导运算均只针对于第二变量：loss function：$f(\theta)=\mathbb{E}\left[\ell\left(y_{n}, \left\langle x_{n}, \theta\right\rangle\right)\right]$
    $$
    \forall(y, \hat{y}) \in\{-1,1\} \times \mathbb{R}, \quad \ell^{\prime}(y, \hat{y}) \leqslant 1, \quad \ell^{\prime \prime}(y, \hat{y}) \leqslant 1 / 4, \quad\left|\ell^{\prime \prime \prime}(y, \hat{y})\right| \leqslant \ell^{\prime \prime}(y, \hat{y})
    $$
   
   
   B4. 输入数据a.s.被常数限制，离差阵被Hessian$(\theta^\ast)$限制，峰度假设的改版：
   $$
    \forall z \in \mathcal{H}, \theta \in \mathcal{H}, \mathbb{E}\left[\ell^{\prime \prime}\left(y_{n},\left\langle\theta, x_{n}\right\rangle\right)^{2}\left\langle z, x_{n}\right\rangle^{4}\right] \leqslant \kappa\left(\mathbb{E}\left[\ell^{\prime \prime}\left(y_{n},\left\langle\theta, x_{n}\right\rangle\right)\left\langle z, x_{n}\right\rangle^{2}\right]\right)^{2}
   $$


</font>
&nbsp;

- **Theorems :**

  <font size=3>
  ***1) Theroem1: A1-6;*** 
   for any constant step-size, $$\mathbb{E}\left[f\left(\bar{\theta}_{n-1}\right)-f\left(\theta_{*}\right)\right] \leqslant \frac{1}{2 n}\left[\frac{\sigma \sqrt{d}}{1-\sqrt{\gamma R^{2}}}+R\left\|\theta_{0}-\theta_{*}\right\| \frac{1}{\sqrt{\gamma R^{2}}}\right]^{2},\text {When } \gamma=1 /\left(4 R^{2}\right), \text { we obtain } \mathbb{E}\left[f\left(\bar{\theta}_{n-1}\right)-f\left(\theta_{*}\right)\right] \leqslant \frac{2}{n}\left[\sigma \sqrt{d}+R\left\|\theta_{0}-\theta_{*}\right\|\right]^{2}$$
   
   
  **ps：可计算得$f\left(\bar{\theta}_{n-1}\right)-f\left(\theta_{*}\right) = \frac{1}  {2}<\bar{\eta}_{n-1}, H \bar{\eta}_{n-1}>, \bar{\eta}_{n-1}=\bar{\theta}_{n-1}-\theta^\ast$**


  ***2) Theorem2: A1-7;*** for any real $p \ge 1$, and for a step-size $\gamma \le 1/12p\kappa R^2, $ we have 
 $$\left(\mathbb{E}\left|f\left(\bar{\theta}_{n-1}\right)-f\left(\theta_{*}\right)\right|^{p}\right)^{1 / p} \leqslant \frac{p}{2 n}\left(7 \tau \sqrt{d}+R\left\|\theta_{0}-\theta_{*}\right\| \sqrt{3+\frac{2}{\gamma p R^{2}}}\right)^{2}$$
   
  <font color=darkorange size=2>
   ps: 最后的bound中不含有关于噪声的信息，在collary中利用Markov不等式得到了一个关于目标的概率截尾不等式。
  </font>
  

   ***3) Theorem3: B1-4*** consider the vector $ζ_n$ obtained as follows: (a)进行n步步长为常数$\frac{1}{2R^2\sqrt{n}}$的averaged SGD得到一个support point$\widetilde{\theta}$
and (b)做n步步长为$1/R^2$的averaged LMS逼近f在support point周围的二次逼近（i.e. one-step estimator). 
   if $n \geqslant\left(19+9 R\left\|\theta_{0}-\theta_{\ast}\right\|\right)^{4}$,
   $$
  \mathbb{E} f\left(\zeta_{n}\right)-f\left(\theta_{*}\right) \leqslant \frac{\kappa^{3 / 2} \rho^{3} d}{n}\left(16 R\left\|\theta_{0}-\theta_{*}\right\|+19\right)^{4}
  $$
  </font>
&nbsp;
- **Technical Skills :**
  
  **1)Theorem 1: A1, A2, A3, A4, A5, A6** 
  <font size=3 color = #00008B> 
  key: $$\left\|H^{1 / 2} \bar{\eta}_{n}\right\|_{p} \leqslant\left\|\frac{1}{n+1} \sum_{i=0}^{n} M_{1}^{j} \eta_{0}\right\|_{p}+\left\|\gamma \sum_{k=1}^{n}\left(\sum_{i=k}^{n} M_{k+1}^{i}\right) \xi_{k}\right\|_{p}$$
   将目标的上界bound分为相互独立的初始设置与噪声的影响，使得在分析时，可以在噪声为0的情况下，利用含初始设定item去bound目标，或者在初始设定完美的情况下(i.e. $\eta_0 = \theta_0 - \theta^\ast = 0$)，利用含$\xi_k$的item进行bound目标。（即对于两个变量，将一个特殊化后，对另一个进行分析）原文：the similarity with bias-variance decomposition。
  </font> 
  
  
  **Step one:** 
 假设没有noise，此处($\eta_n = \theta_n - \theta^\ast$)，利用$\left\|\eta_{n}\right\|^{2}=\left\|\eta_{n-1}\right\|^{2}-2 \gamma\left\langle\eta_{n-1},\left(x_{n} \otimes x_{n}\right) \eta_{n-1}\right\rangle+\gamma^{2}\left\langle\eta_{n-1},\left(x_{n} \otimes x_{n}\right)^{2} \eta_{n-1}\right\rangle$向目标$\langle\bar{\eta}_{n-1}, H\bar{\eta}_{n-1}\rangle$进行靠近, 通过离差阵限制以及$\gamma R^2 \le 1$消去二次形式，化为不等式的迭代类型。直接利用关于$E||\eta_n||^2$的不等式迭代以及凸性，可以得到关于initial condition的bounds。
 
 

  **Step two:** 对于noise进行分析，对于初始值有以下假设：
  <div align='center'>
  <img src = '1_recursion.png' width='200' >
  </div>

  对于迭代序列的新定义：

  <img src = '1_recurrent.png' width='600'>

  寻找关于$\eta_n - \sum^r_{i=0}\eta_n^i$的迭代等式，利用$\mathbb{E}\left\langle\bar{\eta}_{n-1}-\sum_{i=0}^{r} \bar{\eta}_{n-1}^{i}, H\left(\bar{\eta}_{n-1}-\sum_{i=0}^{r} \bar{\eta}_{n-1}^{i}\right)\right\rangle$与$\mathbb{E}\left\langle\bar{\eta}_{n-1}^{r}, H \bar{\eta}_{n-1}^{r}\right\rangle \leqslant \frac{1}{n} \gamma^{r} R^{2 r} d \sigma^{2}$约束$\left(\mathbb{E}\left\langle\bar{\eta}_{n-1}, H \bar{\eta}_{n-1}\right\rangle\right)^{1 / 2}$。
  <font color=darkorange size=2>ps: 像上述迭代式设定的原因，以及为什么要对这个式子做迭代。
  </font>
  
  **Step three:** 合并以上两个bound
&nbsp;

  **2)Theorem 2: A1, A2, A3, A4, A5, A6, A7**<font size=2 color=darkorange>
  *ps: 主干流程还是遵循Theorem1中的初始设置与噪声的分割，其实证明本质过程与1相同，只是涉及由于高阶矩所以会使用到BRP不等式进行相应的处理，看起来比较复杂*
  </font>

  **Step one:** 老样子还是free from noise，与Theorem 1开始的证明方式相同，对于$||\eta_n||$构造迭代式（在理想情况下，$\eta_n$会趋向于0），放缩迭代完成后会得到关键部分$\sum_{k=1}^{n}\langle \eta_{k=1},H\eta_{k-1} \rangle$，与1不同的是此处对于$(x_n \otimes x_n)$的处理有区别，定理一很豪爽地就放到H上去了直接得到结果，定理二这样做与为了得到高阶p时的收敛速度有直接关系：
  $A_{n} \stackrel{\text { def }}{=}\left\|\eta_{n}\right\|^{2}+\gamma \sum_{k=1}^{n}\left\langle\eta_{k-1}, H \eta_{k-1}\right\rangle \leqslant\left\|\eta_{0}\right\|^{2}+\sum_{k=1}^{n} M_{k}$。接下来很自然的就是对于$A_n$与$M_k$的p阶范数处理，其中对于后者处理时用到了BRP不等式：$\sum||M_k||^p \le \sqrt{p}\left\|\sum_{k=1}^{n} \mathbb{E}\left[M_{k}^{2} | \mathcal{F}_{k-1}\right]\right\|_{p / 2}^{1 / 2}+p\left\|\sup _{k \in\{1, \ldots, n\}}\left|M_{k}\right|\right\|_{p}$

  &nbsp;
  **Step two:** 接下来依然是对noise的处理。原文表述：based on the sequences $(\eta^r_n)_n$, we need 
  (a) bounds on the initial setting
  
  (b) a recursion on the magnitude (in $||·||_p\ norm$)of $(\eta^r_n)$ 
  
  (c) a control of the error made in the expansions.

  Bounds on Initial setting: Under assumptions made in Theorem one for perfect initial parameter picking, we have $\eta_{n}^{0}=\gamma \sum_{j=1}^{n}(I-\gamma H)^{n-j} \xi_{j}$, then we have $\sup _{\operatorname{tr} M=1}\left\|\sup _{k \in\{1, \ldots, n\}}\right\| M^{1 / 2} \eta_{k}^{0}\|\|_{p} \leqslant \frac{1}{R} \sqrt{p \gamma R^{2}}(\sigma+\tau \sqrt{p \gamma R^{2}})$

  Recursion on bounds on $\eta_n^r$: <font size=2 color=darkorange> *ps:其中大量运用了关于正定算子trace的不等式：$tr(AB)\le tr(A)tr(B),$ if A and B are both postive operators和峰度假设*
  </font>
  Suppose $$
  A_{r}=\sup _{\operatorname{tr} M=1}\left\|\sup _{k \in\{1, \ldots, n\}}\right\| M^{1 / 2} \eta_{k}^{r}\|\|_{p}
  $$ 构造满足BRP不等式的形式，使用BRP不等式后得到$A_r \le B + C$, 将B和C向着$A_{r-1}$的方向转化，使得不等式变为关于A的迭代。

  &nbsp;

  **Step three:** 将Theorem 1的最后一步的相关item的bound全部向着$A_r$转化，构造迭代也好，直接用$A_r$限制其值也好，总之要与已知的界产生联系。最后合并bound。



  &nbsp;
  
  **3)Theorem 3:**<font size=2 color=darkorange>
  *ps: Two-step procedure：提出该算法的基本思想：由齐次Markov chain的理论，我们可以得到在损失函数为二次时，$\bar{\theta_n}$收敛到的不变分布的均值$\bar{\theta}_r$才等于$\theta^\ast$, otherwise, $\bar{\theta}_n \to \bar{\theta}_r \ne \theta^\ast$。而对于非二次的损失函数，我们可以用二阶的泰勒在some support point处去近似替代，而一个简单的修正想法来源于one-step estimator（summary中有简单介绍）, 此处使用newton迭代是为了逼近一阶导数的零点，而这里的newton迭代过程恰好可以使用stochastic approximation去近似求解。*
  </font><font size=3 color=darkblue> 先明确证明的大致过程与方向：首先我们需要一个support point $\theta_1$（这个有constant-step-size averaged SGD产生）,然后基于该点进行Newton迭代，理论解为$\theta_{2}=\theta_{1}-f^{\prime \prime}\left(\theta_{1}\right)^{-1} f^{\prime}\left(\theta_{1}\right)$, 我们的迭代解定义为$\theta_3$为$\theta_{2}$的近似，最后需要的是bound on $f(\theta_3)-f(\theta^\ast)$,由下列命题提示证明可以朝着将bound分解为$\epsilon_1\ and\ \epsilon_2$。

  <div align='center'>
  <img src = '1_prop.png' width='500' >
  </div>
  </font>

  **Step one:** 实际上，我们很容易看到在这个Two-step procedure的算法中，第一步利用constant-step-size averaged SGD产生的误差$\epsilon_1 = f(\theta_1) - f(\theta^\ast)$完全可以利用Theorem 1中的相关结论控制。实际上我们最主要关心的是第二步产生的误差$\epsilon_2$。
  在对于$\mathbb{E}\left[f\left(\theta_{3}\right)-f\left(\theta_{*}\right) | \mathcal{G}_{1}\right]$进行初步处理时，用了概率论中事件空间划分的小技巧：

  $$
  \begin{array}{c}{A_{1}=\left\{f\left(\theta_{1}\right)-f\left(\theta_{*}\right) \leqslant \frac{1}{16^{2}}(\kappa \rho)^{-1}\right\}=\left\{\varepsilon_{1} \leqslant \frac{1}{16^{2}}(\kappa \rho)^{-1}\right\}} \\ \\ {A_{2}=\left\{\frac{1}{2}\left\langle\theta_{3}-\theta_{2}, f^{\prime \prime}\left(\theta_{1}\right)\left(\theta_{3}-\theta_{2}\right)\right\rangle \leqslant \frac{1}{16}(\kappa \rho)^{-1}\right\}=\left\{\varepsilon_{2} \leqslant \frac{1}{16}(\kappa \rho)^{-1}\right\}}\end{array} $$
  
  划分为$1=1_{A_{1}} 1_{A_{2}}+1_{A_{1}} 1_{A_{2}}^{c}+1_{A_{1}^{c}}$, 目的在于创造使用proposition 1的条件，将bound的限制迅速转化为有关于$\epsilon_1$ and $\epsilon_2$的问题：最后得到的式子中主要含$\epsilon_1$ and $\epsilon_2$不同阶的期望项以及没有被化去的事件的特征函数（后期通过取期望后，利用cauchy-Shwarz不等式化为概率以及其本身对应不等式的特点利用Markov不等式计算概率的上界）

  
  **Step two:** 如上面所说，后面的关键在于对算法第二步产生的$\epsilon_2$的分析，但仔细思考由于我们采用的是averaged LMS去逼近参数$\theta_2$，所以依旧可以利用Theorem 1的相关结论，但是需要考虑的是由于涉及到原函数的不仅仅是本身与一阶导，还有其二阶导，我们需要对于背景设定中的很多东西进行重新定义并且计算上界，以方便框架的移植（这正是A1-6中假设中没有具体设定某个loss函数并且将响应变量用$z_n$表示的原因）：
  $$\begin{aligned} \tilde{x}_{n}=\sqrt{\ell^{\prime \prime}\left(y_{n},\left\langle x_{n}, \theta_{1}\right\rangle\right)} x_{n} \text { and } \tilde{z}_{n}=-\ell^{\prime}\left(y_{n},\left\langle x_{n}, \theta_{1}\right\rangle\right) x_{n}, \text { so that } \\ g(\theta)=f\left(\theta_{1}\right)+\mathbb{E}\left[\frac{1}{2}\left\langle\theta-\theta_{1}, \tilde{x}_{n}\right\rangle^{2}-\left\langle\tilde{z}_{n}, \theta-\theta_{1}\right\rangle\right] \end{aligned}
  $$ $$\begin{array}{l}{\text { We denote by } \theta_{2}=\theta_{1}-f^{\prime \prime}\left(\theta_{1}\right)^{-1} f^{\prime}\left(\theta_{1}\right) \text { the output of the Newton step, i.e., the global minimizer }} \\ {\text { of } g, \text { and } \tilde{\xi}_{n}=\tilde{z}_{n}-\left\langle\theta_{2}-\theta_{1}, \tilde{x}_{n}\right\rangle \tilde{x}_{n} \text { the residual. }}\end{array}
  $$ 
  于是下面的流程与定理1类似，对于残差矩阵与离差矩阵进行上界估计，然后根据这些估计套用Theorem 1的相关结论得出$\mathbb{E}\left[\varepsilon_{2} | \mathcal{G}_{1}\right]$的上界。

  **Step three:** 将在Theorem 1下的$\epsilon_1$与$\epsilon_2$相关结论带入（此处用了很多函数不等式，并在appendix的多个proposition中探究了他们与已知常量的关系）

  &nbsp;

- **Summary :**
  <font size =3>
  1. 证明过程感觉看过了以后，虽然能够理解推导过程，但感觉对于推导的细节记忆不清或者过一段时间以后会忘掉过程，不知道采用写Notes的方法，能不能对此有所改善。
  2. 就这篇文章本身而言，用到的证明方法很多：关于迹的不等式（特别是对于正定对称阵的运用），基本不等式，BRP不等式，Minkowski不等式，Markov不等式，Cauchy-Schwarz不等式，one-step estimator，以及关于self-concordance function的一些性质（其中包括了构造辅助函数，解微分方程证明不等式的方法），以及在特定条件下对于在最优点处Hessian阵的分析……比起以前的文章，后部分的证明方法可能会很大程度上依赖于前面定理的证明或者过程，这篇文章的证明方法的花样更多，值得花更多的时间反复读，更加熟悉。
  3. Harris Recurrent Chain: 将大数定律的收敛与马尔科夫链的平稳分布的均值联系起来：$\bar{\theta}_{n-1} \to \bar{\theta}_r \ a.s.$,其中有$\theta_n \stackrel{d}{\longrightarrow}\theta,\ \bar{\theta}_r = \int\theta\pi_r(d\theta)$, 为利用averaged SGD参数去逼近$\theta^\ast$提供理论基础：不变分布的均值与$\theta^\ast$相等，在某些强假设下，还可以从$\lim _{n \rightarrow \infty} n \mathbb{E}\left[\left(\bar{\theta}_{n}-\theta_{*}\right)^{2}\right]=\operatorname{Var}_{\pi_{\gamma}}\left(\theta_{0}\right)+2 \sum_{k=1}^{\infty} \operatorname{Cov}_{\pi_{\gamma}}\left(\theta_{0}, \theta_{k}\right)$看出右边式子有限，故左边的收敛速度应该为$O(\frac{1}{n})$
  4. 定理1，2中的lemma中对于初始设定的bound大多都是基于算子多项式的运算：正定对称算子级数求和运算，e.g.$\sum_{k=1}^{n-1}(I-\gamma H)^{2 n-2-2 k} H$
  5. note <v, Hv> 为关于v为凸函数，当H为正定矩阵时。
  6. 一般而言，在某些情况下SGD会对initial condition有遗忘性，可以继续探究该方法下的遗忘性条件
  7. 对于递归迭代式，可以尝试用数学归纳法去证明一些命题
  8. 针对于鞅背景&高阶矩设定的BRP不等式（对于p的大小有要求限制）：
  <div align='center'>
  <img src = '1_BRP.png' width='600' >
  </div>
  
  9. $L_p$范数关于p存在单调性，关于p单调增
  
  10. One-step estimator: intended for improving inefficient estimators, to produce a consistent estimator with asymptotic variance equal to the inverse Fisher Information(i.e. usually Cramer-Rao lower Bound when g($\theta$) = $\theta$), we have two main methods: Newton Methods and Method of Scoring, both of which produce a sequence of estimators for approximating UMVUE.
  <div align='center'>
  <img src = '1_newton.png' width='600' >
  </div>

  11. 文章中的损失函数定义为期望形式，而实际操作中损失函数都面对的是单一样本点，是empirical loss。
  
  12. 两次Cauchy-Shwarz不等式：
$\mathbb{E}|X Y Z| \leqslant\left(\mathbb{E}|X|^{2}\right)^{1 / 2}\left(\mathbb{E}|Y|^{4}\right)^{1 / 4}\left(\mathbb{E}|Z|^{4}\right)^{1 / 4}$

  13. 文章中还提到了一种算法，但是其收敛性没有得到证明：
    <div align='center'>
    <img src = '1_al.png' width='600' >
    </div>   可以看出这个式子中其实涉及到两个迭代过程，文中也指出这个算法过程可能与two-scale-step的迭代相关。

  14. 向量函数的高阶导数的一些表示问题 
</font>

#### 5. The Tradeoff of Large Scale Machine Learning

- **Abstract :**

- **Assumptions :**
  
- **Theorems :**
  
- **Technical Skills :**
  
- **Summary :**


