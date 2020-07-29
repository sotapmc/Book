# 配置文件

在配置 Ageing 之前，首先要弄清楚，Ageing 能做些什么。大概有如下几点

- 统计用户的「年龄」数据和相应的「经验」值
- 随着用户的年龄变化执行指令
- 管理指定指令执行所需的最低年龄
- 设计用户年龄的增长规律和趋势
- ...

这些内容都会被添加到配置文件中供给设置，这样，你便可以设置出自己想要的效果。下面，我们会一一列举配置文件中存在的各个项，展示其格式并解释其作用。

### age-commands

```yml
age_commands:
    "年龄 1":
        - "所要执行的指令 1"
        - "所要执行的指令 2"
        - # ...
    "年龄 2":
        - #...
    # ...
```

规定**所有**玩家达到指定的年龄以后，控制台自动执行的指令，允许使用[占位符](#占位符)。使用例：

```yml
age_commands:
    "0":
        - "say Hello, %playername%! Welcome to the Server!"
        - "say Here is your gift!"
        - "give %playername% diamond 5"
    "20":
        - "give %playername% diamond 20"
        # ...
    # ...
```

在这里的指令都会通过控制台执行，因此指令没有任何权限限制，但这也同样意味着无法执行玩家专用的指令。

?> 💡 上述示例中，年龄为 `0` 时所执行的指令，将会在新玩家第一次进入服务器时执行。该功能取代了先前的小工具 [FirstJoinCommand](https://github.com/sotapmc/FirstJoinCommand)。

### max-age

```yml
max_age: # 正整数
```

!> Ageing 目前尚未添加对配置文件中的配置项的值的可用性的检测，因此填入无效之后，可能出现或大或小的不可预料的非常情况。强烈建议你按照规定填写。

规定玩家所能成长到的最高年龄，必须为正整数，且最高不能超过 Java 的整数精度限制（$2^{31} - 1 = 2147483647$）。

### limited-commands

```yml
limited_commands:
  example1: 0
  example2: 0
```

对用户可用的指令进行限制。应遵循 `指令名: 最低年龄` 的格式。例如 `help: 20` 代表须最少 20 岁才可执行 `help` 指令，若未达到年龄，该指令将会被屏蔽，玩家将会收到警告。

!> 若你规定了一个不存在指令的最低年龄，Ageing 仍然会对未达到年龄的人给予警告。例如当规定了 `blablabla123: 20` 时，任何低于 20 岁的玩家在执行该指令时，仍然会收到来自插件的警告，而**不会**收到「该指令不存在」相关的提示。

### command-lowest-limit

```yml
command_lowest_limit: # 非负整数
```

规定能够使用指令的最低年龄。在这个年龄以下将无法使用指令*，即每条指令都会收到警告而不会执行。该配置的优先级高于 `limited-commands`，因此当 `limited-commands` 中出现比该值小的值时，只会按照 `command-lowest-limit` 进行判断。

<small>* 不绝对。请阅读下方的 <code>ignored-commands</code> 了解更多。</small>

### ignored-commands

```yml
ignored_commands:
    - "指令 1"
    - "指令 2"
    - # ...
```

规定不参与年龄限制的指令。处于该列表中的指令将对所有年龄的用户可用。该配置的优先级高于 `limited-commands` 和 `command-lowest-limit`。任何出现在该列表中的指令，都不会受到前两者的限制。

### growth-*

详见[年龄增长原理](/ageing/growth.md)。

## 占位符

### 配置文件占位符

- `%playername%` - 玩家名
- `%uuid%` - 玩家的 UUID

这些占位符只能在配置文件 `config.yml` 中使用。

### PlaceholderAPI 占位符

当 Ageing 被启用时（正常放置在 `plugins` 文件夹中），将自动注册 PlaceholderAPI 占位符。目前支持三种

- `%ageing_age%` - 当前玩家的年龄数值
- `%ageing_experience%` - 当前玩家的总经验值
- `%ageing_experience_to_next%` - 当前玩家距离下一年龄所需的经验值

这些占位符可以在其它支持 PlaceholderAPI 占位符的插件配置中使用，例如 [TrMenu](https://github.com/Arasple/TrMenu)（非广告）。