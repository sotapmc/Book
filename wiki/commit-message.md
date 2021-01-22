# 提交信息规范

为了使信息提交更加规范工整，在这里给出推荐的提交信息规范。通常情况下，使用提交信息规范后，提交信息将变得更易读、更明确。

## 什么是提交信息规范？

提交信息规范是指，在 GitHub 或本地对 Wiki 上的文件进行修改后，提交时所附带的信息的规范。例如，通常情况下我们都习惯于随便写：

```
删去了多余的内容
啊啊啊啊啊啊啊啊啊啊啊
更新完睡觉
更新
新章节：玩家须知
```

然而这些就会造成很多阅读上的问题。为什么？因为提交信息本身是用来描述一个提交所起的具体作用。而如果不加以规范，提交将会变得非常难懂，以至于忘了这个提交到底是在做什么。因此，我们需要对其进行规范。

## 规范简介

当今业界已经有了[一套较为主流的规范](https://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)，经过我们简化后，可以概括为

$$\mathrm{type(scope): msg}$$

令 $t=\mathrm{type}, s=\mathrm{scope}, m=\mathrm{msg}$，上式可表示为

$$t(s):m$$

这便是 Wiki **提交信息规范的一般形式（the Common Form of Commit Info Laws, CFCIL）**，其中 $s$ 可为空。例：

```
fix(plugins): wrong plugin description
fix: bad css rules
feat: add appbar buttons
refactor: rewrite router logic
doc: add description for Filters
```

也就是说，$t$ 代表**当前更改的类型（the Type of Commit）**，$s$ 代表**当前更改的对象或领域（the Scope Affected by Commit）**，$m$ 代表**对改更改的简略介绍（the Message of Commit）**。然而，对于 Wiki 来说，我们并不会出现 `feat`（代表新的 feature，也就是新功能）、`refactor`（重构）等 $t$ 值。为了方便性，我们列出了下面这些在 Wiki 中常用的 $t$ 值及其具体含义。

|$t$|英文全称|含义|
|:-:|:-:|:-:|
|`upd`|update|更新内容。指对以前已经存在的内容的进一步修改和完善|
|`remo`|remove|删除内容。指对以前已经存在的内容的删除或完全移除|
|`meg`|merge|合并内容。既可以指 Git 操作中的 `merge` 性提交，也可以指对多篇文章内容或代码的整合操作|
|`rew`|rewrite|重写内容。指内容上的重构，对以前已经存在的内容的二次改写或彻底重写|
|`doc`|document|新文档。指新内容的添加，必须是以前不存在的内容（对于当前分支来说）|
|`chore`|chore|杂项。指一些并不能用上述 $t$ 值来描述的操作，尽量不使用|

## 注意事项

规范的使用必定有一些注意事项，部分内容引用自阮一峰的[博客文章](https://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)。

1. $\forall m,$ 请遵循
    1. 以动词开头，使用第一人称现在时，比如 `change`，而不是 `changed` 或 `changes`
    2. 第一个字母小写，专有名词可大写
    3. 结尾不加句号（`.` 或 `。`）
2. 请不要混淆 `upd` 和 `doc`。前者是指对现有内容的改动，后者是指新增当前分支所没有的内容（也就是说，当从其它分支迁移内容时，依然符合 `doc`）。
3. 对于 `rew` 和 `upd`，前者优先级更高。重写内容这一行为本身也属于一种 update，但只要符合重写特征，即删去原先内容并重新编写意义大致相同（或用来取代原有内容）的文字，就使用 `rew` 而非 `upd`。
4. 对于 `remo`，不可有任何大规模添加操作。如果只是删除一段文字而没有要加上新内容的打算，可使用 `remo`；而如果删除以后有所添加，请考虑 `rew`。

对 $t$ 值的确定，可以由以下流程图表示（`meg`、`chore` 除外）：

![commit-type-flowchart.png](https://i.loli.net/2021/01/23/QUjEMph7CixKIfy.png)