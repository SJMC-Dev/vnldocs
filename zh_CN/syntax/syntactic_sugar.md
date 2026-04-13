# Vanillang 语法糖

Vanillang 语法糖是指一些特殊的语法形式，它们在编译时会被转换成更基本的语法结构，以提供更简洁、易读或更强大的表达能力。下面列出了一些 Vanillang 中常见的语法糖：

## None 关键字

使用 `None` 关键字可以直接用于实例化一个 `Optional\<T\>` 类型的值，表示一个空值：

```vanillang
let value: Optional<string> = None
```

## 可选类型语法

通过在类型注解后面添加 `?`，可以将一个类型 `T` 标记为可选类型，等价于 `Optional\<T\>`，实际类型也为 `Optional\<T\>`：

```vanillang
let name: string? = None // 等价于 let name: Optional<string> = None
```

## 向上传递异常

在函数体内的完整语句结尾使用 `?`，表示如果该语句抛出异常，则将异常向上传递给调用者：

```vanillang
func getBlockEntityInfo(pos: Vec3) -> Dict {
    let blockEntity = world.getBlockEntity(pos)?
    return blockEntity.toDict()
}
```