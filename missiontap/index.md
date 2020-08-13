# 📕 MissionTap

![](https://img.shields.io/badge/version-1.0-brightgreen)

**MissionTap** 是一个简单的任务系统，分为多种工作模式，这些工作模式都被细化为了配置文件的项目。借助本插件，你可以

- 实现定时随机抽取任务并分配给玩家。
- 设计不同的任务，放入一个永久的「池」中，供给随机抽取；
- 设计特殊任务，利用 `config.yml` 中的开关对其的可见性、可统计性进行管理；
- 设置在任务完成时所执行的指令，几乎可以做任何事；
- 设置在任务完成时所奖励的 Ageing 经验值。

包括但不仅限于以上内容，且在将来该插件将会持续完善。

## 基本使用步骤

1. 安装 [Ageing](//github.com/sotapmc/Ageing) 和 [MissionTap](//github.com/sotapmc/MissionTap) 到 `plugins` 目录中，重新启动服务器。
2. 打开 MissionTap 的数据目录，编辑 `daily-missions.yml` 和 `weekly-missions.yml`，在其中写入任务。具体的格式可以参考[任务格式](/missiontap/structure.md)。
3. 再次重启服务器。
4. 至此即可开始正常使用。可用的指令可查看[指令列表]()。

## 目录

- 🔧 [配置文件](/missiontap/config.md)
- 🏃‍ [任务逻辑](/missiontap/mission.md)
- ⌨ [指令列表](/missiontap/commands.md)
- 📕 [任务格式](/missiontap/structure.md)
- ♻ [刷新逻辑](/missiontap/refresh.md)