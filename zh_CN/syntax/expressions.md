# Vanillang 表达式

Vanillang 表达式是由一个或多个操作数和运算符组合而成的代码片段，用于计算一个值。字面量、变量自身也是表达式。

下面的表格列出了 Vanillang 中常用的表达式类型及其示例：

| 表达式类型     | 用途                           | 示例                                                                             |
| -------------- | ------------------------------ | -------------------------------------------------------------------------------- |
| 算术表达式     | 用于进行数学运算               | `1 + 2`、`num * 3`、`(a - b) / c`                                                |
| 关系表达式     | 用于比较两个值并返回布尔值     | `num > 0`、`player.health <= 10`、`str1.equals(str2)`                            |
| 逻辑表达式     | 用于进行逻辑运算               | `isRaining && player.inDimension("minecraft:overworld)")`、`!isDaytime`          |
| 位运算表达式   | 用于进行位级运算               | `flags & 0x01`、`(permissions >> 2) & 0x07`                                      |
| 条件表达式     | 用于根据条件返回不同的值       | `isRaining ? "Take an umbrella" : "Enjoy the sunshine"`                          |
| 函数调用表达式 | 用于调用一个函数并获取其返回值 | `getPlayerName(player)`、`Math.sqrt(16)`、`world.getBlockState([x, y, z])`       |
| 实例化表达式   | 用于创建一个类的实例           | `Player("Steve")`、`TextDisplay()`、`Array<string>()`                            |
| 成员访问表达式 | 用于访问对象的属性或方法       | `player.health`、`entity?.getName()`、`blockState!.isAir()`                      |
| 数组访问表达式 | 用于访问数组或列表中的元素     | `players[0]`、`scores.get(@n)`、`matrix[1][2]`                                   |
| Lambda 表达式  | 用于定义匿名函数               | `lambda (x) -> x * x`、`lambda (player: Player) -> { return player.health > 0 }` |
| 赋值表达式     | 用于给变量赋值                 | `num = 42`、`str = "Hello, Vanillang!"`、`player.health -= 10`                   |
| 空值合并表达式 | 用于在左值为 None 时返回右值   | `result = value ?? "Default Value"`                                              |