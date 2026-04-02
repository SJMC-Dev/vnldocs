# Vanillang 关键字

Vanillang 关键字具有特殊用途，不可作用标识符，下面的表格列出了已经使用的关键字及其用法示例：

## 变量及常量声明

| 关键字  | 用途               | 示例                                                                 |
| ------- | ------------------ | -------------------------------------------------------------------- |
| `var`   | 声明一个变量       | `var num = 1`、`var str: string = "vnl"`                             |
| `let`   | 声明一个运行时常量 | `let players = @a`、`let marker: Marker = @n[type=minecraft:marker]` |
| `const` | 声明一个编译时常量 | `const PI = 3.14`、`const TNT_EDGE_LENGTH = 0.98`                    |


## 函数与控制流

| 关键字     | 用途                                             | 示例                                                                               |
| ---------- | ------------------------------------------------ | ---------------------------------------------------------------------------------- |
| `func`     | 声明一个函数                                     | `func getPlayerName(player: Player) -> string`                                     |
| `return`   | 从函数中返回值或提前结束函数                     | `return`、`return 0`、`return @a[gamemode=creative]`                               |
| `if`       | 用于条件语句开头                                 | `if (player.inDimension(minecraft:overworld))`、`if (num == 1)`                    |
| `else`     | 用于上一条件不满足时                             | `else return 0`、`else if (world.checkBlockState([-11, 63, 2]))`                   |
| `for`      | 变量循环控制                                     | `for (let i in 0..99)`、`for (let player: Player in players)`                      |
| `while`    | 条件循环控制                                     | `while (n >= 1)`、`while (players.size() != 3)`                                    |
| `label`    | 用于定义循环控制流的标签                         | `label outerLoop`、`label innerLoop`                                               |
| `break`    | 跳出当前循环或跳出循环到标签处                   | `break`、`break outerLoop`                                                         |
| `continue` | 跳出本轮循环迭代                                 | `continue`                                                                         |
| `switch`   | 用于选择语句                                     | `switch (num)`                                                                     |
| `case`     | 用于在 switch 语句中匹配编译时常量值或子类的实例 | `case 1`、`case "Vanillang"`、`case BlockDisplay`、`case TextDisplay`              |
| `when`     | 用于匹配子类实例时提供额外条件                   | `case TextDisplay when display.text.equals({text: "Text Display", color: "gold"})` |
| `context`  | 表示当前函数的命令上下文常量，Dict 类型          | `context={as: @p, at: @s}`                                                         |