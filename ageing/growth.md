# 年龄增长原理

为了使年龄增长具有变化性、可控性，我们在配置文件中加入了三个配置项目 `growth_range_length`、`growth_base_value`、`growth_step_value`。接下来，我们专门解释这三个值对年龄变化的具体影响，以及其它与其有关的事项。

### growth-range-length

```yml
growth_range_length: # 正整数
```

定义每一个成长区间的长度，最小为 $1$。为了便于解释，我们将列出一些具体的数字。在下文中，我们将该值称为 $r$。当 $r=5$ 时，观察

$$ A=\\{ \underbrace{0, 1, 2, 3, 4}_5, \underbrace{5, 6, 7, 8, 9}_5, \underbrace{10, 11, 12, 13, 14}_5, ... \\}$$

这样，大概就可以知道这个 $r$ 到底代表着什么了。特殊地，若 $r=0$，程序将无法正常工作。由于目前正处于开发前期，针对该方面的变量可用性验证并不完善，因此请在设置的时候注意。

为了便于后文论述，在这里引入一个量**区间位** $i$ 用来表示某年龄 $n$ 所在的区间位置。$i$ 的值从 $0$ 开始。例如，当 $r=5, n=1$ 时，易知 $i=0$。一般地，$i$ 可以通过如下计算得到

$$ i=f(n)=\begin{cases}
    0 & n\in[0, r]\\\\
    \frac{n-(n\mathrm{mod}r)}{r} & n\in(r, +\infty)
\end{cases}$$

- 当 $r=5, n=1$ 时，满足 $0\lt{n}\lt5$，则 $i=0$
- 当 $r=5, n=9344$ 时，满足 $n\gt5$，则 $i=\frac{9344-(9344\mathrm{mod}5)}{5}=1868$
- 当 $r=5, n=10805$ 时，满足 $n\gt5$，此时易知 $n\mathrm{mod}5=0$，则 $i=\frac{10805-(10805\mathrm{mod}5)}{5}=\frac{10805}{5}=2161$

通常我们把 $i$ 的值作为该年龄区间的位置。对于每一个合理存在的 $n$，我们都称此时 **$n$ 位于第 $i$ 区间**。

!> 实际上，当 $n\gt{r}$ 时，$i=f(n)=\lfloor\frac{n}{r}\rfloor$。

### growth-base-value

```yml
growth_base_value: # 正整数
```

定义成长基准值，最小为 $1$。该值确定了在玩家 $A$ 的年龄在第 $0$ 区间内时，每长一岁所需要的经验值 $e_b$。随着 $A$ 的年龄增长，后续所有的经验值 $e_x$ 都会在该值基础上进行叠加。对于该值更详细的作用，请参考下文的 [growth-step-value](#growth-step-value)。

### growth-step-value

```yml
growth_step_value: # 正整数
```

定义成长叠加值，最小为 $1$。该值确定了当玩家 $A$ 的年龄属于除第 $0$ 区间外的任何区间时，每成长一岁所需要的经验值 $e_x$ 相对于基准值 $e_b$ 的关系。我们通常称该值为 $s$。

引入 $s$ 后，我们可以计算 $e_x$ 的值。一般地，我们有

$$e_{x}=g(n)=\begin{cases}
    e_b & n\in[0, r]\\\\
    e_b+si & n\in(r, +\infty)
\end{cases}$$

其中 $i$ 为上文中提到的区间位。下面综合上述内容举出一些例子。

**当 $r=5, e_b=200, s=150$ 时**

- 当 $n=2$ 时，$i=1$，则 $e_x=e_b=200$
- 当 $n=5$ 时，$i=2$，则 $e_x=e_b+si=200+150\times1=350$
- 当 $n=100$ 时，$i=20$，则 $e_x=e_b+si=200+150\times20=3200$
- 当 $n=9998$ 时，$i=1999$，则 $e_x=e_b+si=200+150\times1999=300050$
- 当 $n=823761248$ 时，$i=164752249$，则 $e_x=e_b+si=200+150\times164752249=24712837550$

既然所有的必要量都齐全了，那么我们引入最后一个量**总经验** $e_t$。当 $n>r$ 时，总经验的求法将每个区间内所含经验总量 $e_{x_m}r$ 分别加起来，再加上当前年龄 $n$ 与该区间的最小年龄 $ir$ 的差值所形成的范围内所含的经验总量 $e_k$。

$$e_k=e_x(n-ir)=e_xn\mathrm{mod}r$$

$$e_t=e_{x_1}r+e_{x_2}r+e_{x_3}r+...+e_{x_m}+e_k$$

明显地，当 $n$ 恰好为 $r$ 的倍数时，$e_k=0$。形象地，我们可以用如下方式来表达 $e_t$ 的具体求法。首先，由于

$$ A=\\{ \underbrace{0, 1, 2, 3, 4}_5, \underbrace{5, 6, 7, 8, 9}_5, \underbrace{10, 11, 12, 13, 14}_5, ... \\}$$

所以我们可以将所有的生长所需经验值表达为

$$ E=\\{ \underbrace{200, 200, 200, 200, 200}_5, \underbrace{350, 350, 350, 350, 350}_5, \underbrace{500, 500, 500, 500, 500}_5, ...\\} $$

<small>这个集合不标准，因为含有重复的元素。因此，我们称它为「数组」。</small>

**如何看**：例如，从 $1$ 岁长至 $2$ 岁所需要的经验值为该数组的第二个元素 $200$；从 $n-1$ 岁长至 $n$ 岁所需要的经验值为该数组的第 $n$ 个元素 $e_{x_n}$。

!> 实际上，在这里有更好更形象的表达形式。由于 Mathjax 不支持这样的 $\LaTeX$，因此无法呈现在此。![](https://i.loli.net/2020/07/27/Y8Hok4gbBAIpxts.png)

其中 $200$、$350$、$500$ 这样的数字均为求得的 $e_x$。设到第 $n$ 岁时所需要的总经验值为 $t$，假设此时 $n=5$，有 $t=200+200+200+200+200=1000$；假设此时 $n=14$，有 $t=200+200+200+200+200+350+350+350+350+350+350+500+500+500+500=4750$

至此，我们发现若 $n$ 在第 $k$ 区间内（$k>0$），则 $t$ 一定为从 $0$ 至 $k-1$ 区间内所有的经验值与「剩下的」经验值之和。我们将上面的算式写成简便形式便能体现这一点

$$ t=200\times5+350\times5+500\times4 $$

回过头看，这个式子正对应了

$$ e_t=e_{x_1}r+e_{x_2}r+e_k $$

其中

$$ e_k=e_x(n-ir)=500\times(14-2\times5)=500\times4 $$

这一方法在编程中的具体实现是利用 `for` 循环，依次求出每一个 $e_xr$ 后相加。