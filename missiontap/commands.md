# 指令列表

以下所有的指令均以 `/mt` 或 `/missiontap` 开头。

|指令|缩写|参数|含义|备注|
|:-:|:-:|:-:|:-:|:-:|
|`weekly`|`w`|-|打开周任务菜单|`require-acceptance` 为 `false` 时不可用|
|`daily`|`d`|-|打开日任务菜单|`require-acceptance` 为 `false` 时不可用|
|`special`|`s`|-|打开特殊任务菜单|`special-missions` 为 `false` 时不可用|
|`inprogress`|`i`|-|查看已接受的任务、提交任务|-|
|`reload`|-|-|重载插件配置文件、菜单和任务|-|
|`init`|-|-|初始化或更新当前配置的基本数据|-|
|`about`|-|-|查看插件关于信息|-|

?> `about` 指令没有权限，无法设置，所有人都可以使用。

## 临时指令

临时指令是指还未完全完工的指令集中，已经可以使用的指令。

|指令|权限|含义|
|:-:|:-:|:-:|
|`player <玩家名> clear-submittion`|`.player`|清空玩家的任务提交记录|

## 权限

以下所有的权限均以 `missiontap.` 开头。

|权限|对应指令|适应人群|是否已默认给予|
|:-:|:-:|:-:|:-:|
|`weekly`|`/mt weekly`, `/mt w`|普通玩家|✔|
|`daily`|`/mt daily`, `/mt d`|普通玩家|✔|
|`inprogress`|`/mt inprogress`, `/mt i`|普通玩家|✔|
|`special`|`/mt special`, `/mt s`|普通玩家|✔|
|`reload`|`/mt reload`|管理员|-|
|`init`|`/mt init`|管理员|-|
|`all`|全部|管理员|-|

默认给予的权限，在没有使用权限管理插件（如 LuckPerms）专门设置之前，会尽可能默认给到指定玩家。如果发现默认情况下的权限异常，请尝试手动设置。对于 `missiontap.all` 权限，一旦设置为 `true`，指定人群或个人则可以访问 MissionTap 的所有指令。

在取消该权限的时候请注意（以 LuckPerms 为例）区分 `set ... false` 和 `unset` 的区别。

```minecraft
/lp <user|group> <对象> permission set missiontap.all false
```

该指令代表**不允许使用 MissionTap 所有指令**。

```minecraft
/lp <user|group> <对象> permission unset missiontap.all
```

该指令代表从对象中移除该节点。详细信息可通过 `/lp <user|group> <对象> permission info` 来查看。