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
# 等价于 let name: Optional<string> = None
let name: string? = None
```

## 向上传递异常

在函数体内的完整语句结尾使用 `?`，表示如果该语句抛出异常，则将异常向上传递给调用者：

```vanillang
func getBlockEntityInfo(pos: Vec3) -> Dict {
    let blockEntity = world.getBlockEntity(pos)?
    return blockEntity.toDict()
}
```

## 枚举模式定义

使用 `enum` 关键字可以定义一个枚举模式，和传统的枚举值相比，枚举模式的每个成员都可以有一个或多个关联值，并且在使用时可以通过模式匹配来解构这些关联值。在 Vanillang 中，枚举模式的本质是一个类，其成员为该类的子类。下面给出一个枚举模式的示例：

```vanillang
enum Result {
    Success(value: string)
    Failure(error: string)
}

#*
    上述代码等价于：

    class Result {}

    class Success extends Result {
        value: string
        func init(value: string) {
            this.value = value
        }
    }

    class Failure extends Result {
        error: string
        func init(error: string) {
            this.error = error
        }
    }
*#

func processResult(result: Result) -> void {
    # switch 语句模式匹配成功时，会自动进行向下类型转换，确保可以访问枚举模式的关联值
    switch (result) {
        case Success when result.value.equals("OK") -> {
            world.print("Operation succeeded with value: " + result.value)
            result.callback()
        }
        case Failure ->  world.print("Operation failed with error: " + result.error)
        default -> world.print("Unknown result")
    }
}
```