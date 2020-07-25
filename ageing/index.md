# Ageing

![](https://img.shields.io/badge/version-extraBeta-aaa)

**Ageing** 是一个以「年龄」为主题的简单等级系统，同时也是将来 SoTap 的大插件体系的重要基础。Ageing 可以用来通过一个统一的量（例如「年龄」）来规划服务器内各项事务的可执行性，例如达到 X 岁后可传送至 X 世界、可执行 X 命令，甚至可以影响到玩家的饮食、交通、发言等各个一般情况下涉及不到的方面。

## 基本概念

<figure style="text-align: center">
    <img src="https://i.loli.net/2020/07/25/UMwNLlBk23hHKWj.png">
    <figcaption>遵循 CC BY-NC-ND 4.0</figcaption>
</figure>

首先需要强调的一点是，Ageing 的功能**非常好实现**（但需要多久就不确定了），我们创造 Ageing 是为了能够更好地规划 SoTap 的插件体系。

Ageing 最初的想法，是以一种类 mcMMO 的形式，从各个方面对玩家进行评估，汇成一个统一的量，例如年龄。然后再基于这个年龄进行许多配置，使其能够影响到玩家的游玩内容，营造一种「年龄越高，内容越丰富，所能做的事情越多」的类似成长的效果。对于具体的讨论，可以参考 [#4](https://github.com/sotapmc/Discussion/issues/4)。

而后来，我们又认为 Ageing 的这种将众多复杂的评估方式整合在一个插件里，既要「计算」，又要「统计」，显得很复杂。与其这样，倒不如把每个方面的评估内容抽出来，然后再另外花一番心思把它做好。也就是说，当这些功能放在 Ageing 中时，就会显得「复杂」，制作也不会那么认真和仔细，因为这不是重点；而当把它拿出来时，看法就变成了「丰富」，制作也会更加用心，因为它是独立的。更重要的是，它可以充当 SoTap 围绕 Ageing 的插件生态的一部分。

那么，Ageing 的基本概念就显而易见了。它是一种核心，是数据的最终集合。其它的插件通过属于自己的逻辑对用户进行定向（定方面）评估，然后再将不规则数据按照自己的方式量化传递给 Ageing，Ageing 则负责将这些数据转化为一个统一量，并允许用户根据这个统一量来规划玩家的行为。值得注意的一点是，这个模式实际上与 Ageing 的初衷并无很大的差异，但实际做起来，Ageing 的内容则是完全的不同。

## 拓展阅读

- [Ageing 的 GitHub 仓库](https://github.com/sotapmc/Ageing)
- 讨论 [#4](https://github.com/sotapmc/Discussion/issues/4)（Ageing 的原构思）
- 讨论 [#6](https://github.com/sotapmc/Discussion/issues/6)（Ageing 及其生态的现有构思）