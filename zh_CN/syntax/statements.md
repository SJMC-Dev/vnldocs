# Vanillang 语句

Vanillang 语句用于执行一个操作或控制程序的流程。一个表达式可以单独作为一个语句，也可以与其他表达式组合成一个更复杂的语句。
  
下面的表格列出了 Vanillang 中常用的语句类型及其示例：

| 语句类型     | 示例                                                                            |
| ------------ | ------------------------------------------------------------------------------- |
| 变量声明语句 | `var num = 1`、`let players = @a`、`const PI = 3.14`                            |
| 函数声明语句 | `func getPlayerName(player: Player) -> string`                                  |
| 条件语句     | `if (num > 0) { ... } else { ... }`                                             |
| 循环语句     | `for (let i in 0..9) { ... }`、`while (n >= 1) { ... }`                         |
| 跳转语句     | `break`、`continue`、`return`、`switch`、`case`                                 |
| 表达式语句   | `player.health -= 10`、`result = value ?? "Default Value"`                      |
| 块语句       | `if (num > 0) { ... }` 中的 `{ ... }`                                           |
| 其他语句     | `label`、`reload` 等特殊用途的语句                                              |
| 注释语句     | `// 这是单行注释`、`/* 这是多行注释 */`                                         |
| 类型声明语句 | `class GameStatus`、`interface Data`、`enum Color`、`type NamespaceId = string` |
| 导入语句     | `import vanillang.ui`                                                           |
| 导出语句     | `export func getPlayerName(player: Player) -> string`                           |