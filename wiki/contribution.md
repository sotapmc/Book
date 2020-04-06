# 贡献

我们接受所有 SoTap 玩家对 Wiki 的贡献，目前我们一共有两种进行贡献的方式。在进行贡献之前，请确保你已经满足以下条件：

- 你已入服超过 1 周，且对服务器内的情况较为熟悉；
- 你拥有查阅其它插件 Wiki 的能力；
- 你拥有良好的文字表达能力；
- 你已经阅读了[基本编写规范](/wiki/manual.md)

## 方式

### 自我提交

自行提交。如果你是开发组成员，则可以直接通过 GitHub 网站或者本地编辑对文件做出更改后提交；如果你不是开发组成员，则可以通过 Fork 之后进行更改，发起 Pull Request 完成提交。以下我们介绍这两者的步骤。

#### 直接编辑后提交

##### 网页在线编辑

!> 在线编辑有因登录 Token 过期以后导致数据丢失的风险，因此建议你采用下面的「本地编辑」

打开 SoTap Wiki 的 GitHub 仓库页面 <https://github.com/sotapmc/SotapWiki>，点击你所要修改的文件（下图以 `index.md` 为例）

![](https://i.loli.net/2020/04/06/uL7jJrYmOhaR9FU.jpg)

点击以后即可打开该文件。需要注意的是，GitHub 自带 Markdown 解析功能，因此当你打开一个 `.md` 文件时，第一时间呈现出来的并不是它的源码，而是它经过解析和排版后的结果。若要开始编辑，点击「铅笔」图标。

![](https://i.loli.net/2020/04/06/TP4JOXtn7Z5dceC.jpg)

之后就可以开始写作了。图中使用红色线条标注的是「编辑」视图，使用橙色线条标注的是「预览」视图。编辑完成以后，点击「Preview Changes」即可不提交查看效果。

![](https://i.loli.net/2020/04/06/2gUKq59NWDbfJRE.jpg)

若要提交，请下滑到页面的最底部

![](https://i.loli.net/2020/04/06/nzkyLU2ZviGfS63.jpg)

共有两个栏目可以填写，其中上面的（使用红色方框标注）为对本次提交的简短介绍信息，下面的（使用橙色方框标注）为对本次提交的补充介绍信息。这两者都是选填，但是我们建议每次提交一定要填写前者来为本次提交加以注释，便于日后进行查阅。至于「简短介绍信息」和「补充介绍信息」有什么区别，请看下图：

![](https://i.loli.net/2020/04/06/RvrZDEajL4q31GO.jpg)

图中红色线条标注的就是「简短介绍信息」，下方橙色线条标注的就是「补充介绍信息」。简短介绍信息会显示在 Log 中，补充介绍信息则需要手动操作才可以显示来。这也是为什么我们要求前者必填。

写好介绍以后，点击绿色的「Commit Changes」按钮即可完成提交，对 Wiki 的更改将在 5 分钟之内生效。如果没有及时生效请联系管理员寻求协助。

##### 本地编辑

?> ✅ 本地编辑是我们所推荐的编辑方式，你可以选择喜欢的编辑器，并无需担心数据丢失

首先使用 Git 来 `clone` 该项目。

```bash
$ git clone git@github.com:sotapmc/SotapWiki
```

`clone` 完毕以后即可开始编写。打开 `clone` 的 SotapWiki 目录，对任意文件进行修改后，使用 `git status` 查看更改状态。再进行如下操作完成提交

```bash
git add <文件名> # 文件名可包含多个，或者直接使用 * 通配符代表所有文件
git commit -m "简短介绍" # 相当于上文中介绍的红色部分
git push origin master # 上传更改，需要互联网连接，如果没有网络可以暂时不上传
```

!> **注意事项**<br>
在进行最后一步 `git push` 之前，请确保项目在你进行编辑的过程中没有人提交任何改动。否则，你需要在 `git push` 之前执行一遍 `git pull origin master` 来同步更改

#### 通过 Pull Request 提交

首先 Fork 本项目。点击项目右上角的「Fork」按钮后，选择你的账号。

![](https://i.loli.net/2020/04/06/t4vGIe38Ohqx5mk.png)

![](https://i.loli.net/2020/04/06/ZNznElHcyMaBxrf.jpg)

选择完毕后，等待 Fork 成功。然后按照上一小节中介绍的「网页在线编辑」或「本地编辑」方法进行编辑和提交即可，唯一的区别是此时你操作的是 Fork 后的仓库而不是原仓库。

![](https://i.loli.net/2020/04/06/fU6shNrXHznMxLR.jpg)

完成编辑并提交以后，在自己的 Fork 项目页面点击「New Pull Request」发起新的 Pull Request。

![](https://i.loli.net/2020/04/06/8kj6SGcs2auWzQb.jpg)

<div class="tip-section">
    <p>在这里显示了一条信息：</p>
    <blockquote>
        This branch is 1 commit ahead of sotapmc:master
    </blockquote>
    <p>它的意思是，当前的提交位于 sotapmc 的 master 分支之前。更通俗易懂地说，你当前对 Fork 中做出的更改是「超前于」原项目一次的。当你第二次提交、第三次提交，这个数字将会递增。但是当在这途中有其它人更改了一些文件，那么将会显示 <em>and ~ commit behind of ...</em>
</div>

点击以后将会跳转到这个页面。在发起 Pull Request 之前，GitHub 会自动对比 Fork 和主项目之间的区别。如果没有任何冲突，将会显示「✔ Able to merge」。而如果有冲突，则会显示有 Conflicts，此时仍然可以尝试进行提交，我们会尝试对冲突进行修复。

![](https://i.loli.net/2020/04/06/WuD8sFAoYfXdaJ9.jpg)

非必要情况请不要更改上方的 `base repository` 和 `head repository`。一切就绪后，点击 「Create pull request」，此时会打开一个留言框，你可以在此写一些详细的介绍或者留言，也可以选择不写。

![](https://i.loli.net/2020/04/06/f4zqJhutU6HogXD.jpg)

完成之后，点击「Create pull request」正式完成创建。至此，你可以在主项目的 Pull Request 列表中看到你所发送的申请。

![](https://i.loli.net/2020/04/06/l2oLVYjiPCsTzSJ.jpg)

当我们看到并 Review 以后就会将您的更改进行 Merge（合并），随后你的更改就会出现在 Wiki 上。

### 联系 Wiki 贡献者

如果您认为以上操作均太麻烦，不适合自己，则可以联系 Wiki 贡献者进行提交。目前我们的贡献者已经列出在了[这里](/wiki/contributors.md)。需要注意的是，Wiki 贡献者可以根据情况进行无偿或者有偿提交（仅限游戏币交易）。