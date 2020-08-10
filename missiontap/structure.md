# 任务格式

```yml
object: # 该任务的独特键名，不能重复
    name: "Test" # 该任务的名称，支持 & 开头彩色代码
    lore: # 该任务的介绍，支持 & 开头的彩色代码
    - "First line"
    - "Second line"
    - "Third line"
    age-exp: 100 # 该任务完成后所奖励的 Ageing 经验值，若不需要可设置为 0 或者删除该项
    rewards: # 该任务完成后所执行的指令。允许使用占位符
    - "say Hello World!"
    - "lp player %playername% permission set deluxetags.tag.test"
    blockbreak: # 该任务在方块破坏方面的要求
        DIAMOND_BLOCK: 50 # 方块名称: 个数
        DIRT: 1000
    breeding: # 该任务在生物繁殖方面的要求
        HORSE: 5 # 生物名称: 个数
        SHEEP: 100
    collecting: # 该任务在收集方面的要求
        WHEAT: 100 # 物品名称: 个数
        WHEAT_SEED: 1000
    combat: # 该任务在生物击杀方面的要求
        PHANTOM: 200 # 生物名称：个数
        SQUID: 100
    crafting: # 该任务在合成方面的要求
        IRON_AXE: 56 # 物品名称：个数
        ICE: 25 # <-请不要添加无法合成的物品名称！
```

支持的占位符

- `%playername%` - 玩家名称
- `%uuid%` - 玩家 UUID

对于各个任务中的名称，例如方块名称、物品名称、生物名称，可以参考 Spigot 的 Javadoc（无技术含量）

- [方块和物品名称](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html)
- [生物名称](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/EntityType.html)

## 关于任务类型

当前 MissionTap 支持五种任务类型，分别是**收集**（`collecting`）、**破坏**（`blockbreak`）、**合成**（`crafting`）、**击杀**（`combat`）、**繁殖**（`breeding`）。

- **收集**要求玩家拾起一定量的物品。每拾起一个物品都会被记录，但不会记录那些被玩家丢出的物品，包括死亡掉落、主动丢弃等。
- **破坏**要求玩家破坏一定量的方块。方块可以是任何可破坏的方块，包括麦子等农作物。
- **合成**要求玩家合成一定量的物品。每合成一个物品都会被记录。
- **击杀**要求玩家击杀一定数量的生物。每击杀一个生物都会被记录，但不会记录击杀玩家。
- **繁殖**要求玩家繁殖一定量的生物。每繁殖一对生物都会被记录。
  - 即将添加的特性：繁殖一个生物之后五分钟内若有击杀该生物的行为，将从繁殖的任务数值中扣除相应的数量，但击杀的任务数值不会受到影响。