# Vanillang 关键字

Vanillang 关键字具有特殊用途，不可作用标识符，下面的表格列出了已经使用的关键字及其用法示例：

## 变量及常量声明

| 关键字  | 用途               | 示例                                                                 |
| ------- | ------------------ | -------------------------------------------------------------------- |
| `var`   | 声明一个变量       | `var num = 1`、`var str: string = "vnl"`                             |
| `let`   | 声明一个运行时常量 | `let players = @a`、`let marker: Marker = @n[type=minecraft:marker]` |
| `const` | 声明一个编译时常量 | `const PI = 3.14`、`const TNT_EDGE_LENGTH = 0.98`                    |


## 函数与控制流

| 关键字     | 用途                                             | 示例                                                                                    |
| ---------- | ------------------------------------------------ | --------------------------------------------------------------------------------------- |
| `func`     | 声明一个函数                                     | `func getPlayerName(player: Player) -> string`                                          |
| `return`   | 从函数中返回值或提前结束函数                     | `return`、`return 0`、`return @a[gamemode=creative]`                                    |
| `if`       | 用于条件语句开头                                 | `if (player.inDimension(minecraft:overworld))`、`if (num == 1)`                         |
| `else`     | 用于上一条件不满足时                             | `else return 0`、`else if (world.checkBlockState([-11, 63, 2], minecraft:grass_block))` |
| `for`      | 变量循环控制                                     | `for (let i in 0..99)`、`for (let player: Player in players)`                           |
| `while`    | 条件循环控制                                     | `while (n >= 1)`、`while (players.size() != 3)`                                         |
| `label`    | 用于定义循环控制流的标签                         | `label outerLoop`、`label innerLoop`                                                    |
| `break`    | 跳出当前循环或跳出循环到标签处                   | `break`、`break outerLoop`                                                              |
| `continue` | 跳出本轮循环迭代                                 | `continue`                                                                              |
| `switch`   | 用于选择语句                                     | `switch (num)`                                                                          |
| `case`     | 用于在 switch 语句中匹配编译时常量值或子类的实例 | `case 1`、`case "Vanillang"`、`case BlockDisplay`、`case TextDisplay`                   |
| `when`     | 用于匹配子类实例时提供额外条件                   | `case TextDisplay when display.text.equals({text: "Text Display", color: "gold"})`      |
| `context`  | 表示当前函数的命令上下文常量，Dict 类型          | `context={as: @p, at: @s}`                                                              |
| `void`     | 表示函数没有返回值                               | `func onLoad() -> void`                                                                 |
| `native`   | 表示函数是原生函数，没有 Vanillang 实现          | `native func getPlayerProfile(player: Player) -> Dict`                                  |
| `callee`   | 表示当前函数本身                                 | `return n * callee(n-1)`                                                                |
| `in`       | 用于遍历可迭代对象                               | `for (let i in 0..9)`                                                                   |
| `reload`   | 用于重新加载当前数据包，必须在函数体内使用       | `func reloadDataPack() -> void { reload }`                                              |

## 类型系统与面向对象

| 关键字       | 用途                                                       | 示例                                                                                                            |
| ------------ | ---------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `class`      | 声明一个类                                                 | `class GameStatus`、`class EntityDetector<T>`                                                                   |
| `interface`  | 声明一个接口                                               | `interface Data`                                                                                                |
| `type`       | 重命名一个类型                                             | `type NamespaceId = string`                                                                                     |
| `enum`       | 声明一个枚举类型                                           | `enum Color`、`enum Gamemode`                                                                                   |
| `extends`    | 用于继承一个基类                                           | `class Player extends Entity`、`class HopperBlockEntity extends BlockEntity`                                    |
| `implements` | 用于实现一个或多个接口                                     | `class Text implements Data`                                                                                    |
| `this`       | 用于指代当前实例对象                                       | `this.id = id`                                                                                                  |
| `super`      | 用于指代上一层基类                                         | `super.getName()`                                                                                               |
| `private`    | 用于声明私有成员                                           | `private id: string` `private func stepOnce() -> void`                                                          |
| `public`     | 用于声明公有成员，可省略                                   | `public func getName() -> string`                                                                               |
| `readonly`   | 用于标识一个不可变类型或纯函数                             | `readonly func getUuid() -> string`、`let text: readonly Text`、`func parseText(text: readonly Text) -> Result` |
| `static`     | 用于标识一个静态成员                                       | `static gameStatus: string`                                                                                     |
| `instanceof` | 用于判断一个实例是否为某个类或其子类，或为某个接口的实现类 | `if (player instanceof Entity)`                                                                                 |
| `final`      | 用于声明一个类不能被继承                                   | `final class World`                                                                                             |
| `override`   | 用于标识一个成员函数覆盖了基类的同名函数                   | `override func getName() -> string`                                                                             |

## 字面量关键字

| 关键字  | 用途       | 示例                             |
| ------- | ---------- | -------------------------------- |
| `true`  | 字面值为真 | `let areAllPlayersOnline = true` |
| `false` | 字面值为假 | `return false`                   |

## 模块关键字

| 关键字   | 用途                                                           | 示例                                                                                        |
| -------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `import` | 用于导入一个标识符                                             | `import vanillang.math.*`、`import vanillang.ui.TextDisplayUi`                              |
| `export` | 用于导出一个标识符                                             | `export class Entity`、`export vanillang.std.Gamemode`                                      |
| `as`     | 用于重命名一个导入或导出的标识符，不能与 * 搭配使用            | `import vanillang.ui.ItemDisplayUi as Button`、`export class VanillangResult {} as Result`  |
| `module` | 用于路径开头，表示当前模块，同时声明这是一个相对路径           | `export module.*`、`export module.{ScoreboardTimer as Timer, ScoreboardCounter as Counter}` |
| `parent` | 用于在相对路径中表示上一级的包名                               | `import module.parent.parent.foo.Bar as Baz`                                                |
| `*`      | 用于导入或导出一个模块下的所有可导出标识符，不能与 as 搭配使用 | `import vanillang.ui.*`、`export module.*`                                                  |
| `self`   | 用于表示当前包或模块                                           | `import vanillang.ui.{self, ItemDisplayUi, TextDisplayUi}`                                  |