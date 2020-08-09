# 指令列表

以下所有的指令均以 `/mt` 或 `/missiontap` 开头，所有的权限均以 `missiontap` 开头。

|指令|缩写|参数|权限|含义|备注|
|:-:|:-:|:-:|:-:|:-:|:-:|
|`weekly`|`w`|-|`.weekly`|打开周任务菜单|`require-acceptance` 为 `false` 时不可用|
|`daily`|`d`|-|`.daily`|打开日任务菜单|`require-acceptance` 为 `false` 时不可用|
|`special`|`s`|-|`.special`|打开特殊任务菜单|`special-missions` 为 `false` 时不可用|
|`reload`|-|-|`.reload`|重载插件配置文件、菜单和任务|-|
|`init`|-|-|`.init`|初始化或更新当前配置的基本数据|-|
|`inprogress`|`i`|-|`.inprogress`|查看已接受的任务、提交任务|-|
|`about`|-|-|-|查看插件关于信息|-|

## 临时指令

临时指令是指还未完全完工的指令集中，已经可以使用的指令。

|指令|权限|含义|
|:-:|:-:|:-:|
|`player <玩家名> clear-submittion`|`.player`|清空玩家的任务提交记录|