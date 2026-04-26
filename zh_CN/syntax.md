# Vanillang 语法

## 概述

Vanillang 的语法设计旨在提供一种简洁、易读且功能强大的编程语言，适用于 Minecraft 原版开发。Vanillang 的语法借鉴了多种现代编程语言的特点，同时结合了 Minecraft 数据包的特定需求，形成了一套独特的语法体系。

Vanillang 的语法主要包括以下几个方面：
- 模块与包
- 声明
- 表达式
- 语句
- 注释

## 模块与包

Vanillang 定义一个模块为一个后缀名为 `.vnl` 的源代码文件，一个包为一个目录，包内可以包含多个模块。模块和包的命名规则与标识符相同，但不能使用关键字和保留字。其中，根包定义为向编译器提供的指定目录。

可以使用 `import` 声明导入一个包、模块或标识符：
- 导入的标识符必须是使用 `export` 声明导出的。导入时可以使用 `as` 关键字为导入的标识符指定一个别名，或者使用 `*` 导入一个包或模块内的所有导出标识符。
- 导入模块时，可以使用模块名访问模块内的导出标识符，例如 `import vanillang.math` 后可以使用 `math.PI` 访问 `math` 模块内的 `PI` 常量；也可以使用 `as` 关键字为模块指定一个别名，例如 `import vanillang.math as m` 后可以使用 `m.PI` 访问 `math` 模块内的 `PI` 常量。
- 导入包时，可以使用包名访问包内所有模块的导出标识符，例如 `import vanillang` 后可以使用 `vanillang.ui.TextDisplayUi` 访问 `vanillang` 包内的 `ui` 模块内的 `TextDisplayUi` 类；也可以使用 `as` 关键字为包指定一个别名，例如 `import vanillang as vnl` 后可以使用 `vnl.ui.TextDisplayUi` 访问 `vanillang` 包内的 `ui` 模块内的 `TextDisplayUi` 类。需要注意的是，导入包时不能使用 `*` 导入包内的所有模块，`*` 仅适用于导入标识符。

可以使用 `export` 声明导出一个标识符，导出的标识符可以被其他模块导入使用。导出时可以使用 `as` 关键字为导出的标识符指定一个别名，指定别名后，在 `import` 声明中只能使用别名导入该标识符，不能使用原名导入该标识符。

导入声明只能出现在模块顶层，不能出现在其他任何地方。导入声明的作用域为整个模块，即在模块内的任何位置都可以使用导入的标识符。 导入声明的执行顺序为从上到下，导入声明会按照它们在模块中的出现顺序依次执行。

导出声明只能出现在模块结尾，不能出现在其他任何地方。

## 声明

Vanillang 支持以下几种声明：
- 变量声明
- 函数声明
- 类型声明
- 属性声明
- 方法声明
- 模块导入声明
- 模块导出声明

声明可以使用元数据进行修饰，元数据是一些供编译器识别并影响编译器行为的标记，可以用于标记已弃用的元素、实验性的元素或禁用警告等。元数据声明必须出现在一个声明的前面，并且与该声明之间只能有一个换行符。

下面给出声明的产生式：

```ebnf
Declaration ::= [ Metadata <NEWLINE> ] (VariableDeclaration | FunctionDeclaration | TypeDeclaration | PropertyDeclaration | MethodDeclaration | ImportDeclaration | ExportDeclaration);

VariableDeclaration ::= ('var' | 'let' | 'const') Identifier [':' Type] '=' Expression;
FunctionDeclaration ::= 'func' Identifier '(' [ParameterList] ')' ['->' (Type | 'void')] Block;
TypeDeclaration ::= ClassDeclaration | InterfaceDeclaration | EnumDeclaration | TypeAliasDeclaration;
PropertyDeclaration ::= [ 'private' | 'public' ] [ 'static' ] Identifier ':' Type ['=' Expression];
MethodDeclaration ::= [ 'private' | 'public' ] [ 'static' ] 'func' Identifier '(' [ParameterList] ')' ['->' (Type | 'void')] [Block];
ImportDeclaration ::= 'import' ImportPath;
ExportDeclaration ::= 'export' ExportList;
Metadata ::= 'metadata' '(' MetadataTerm (',' MetadataTerm)* ')';

Type ::= [ 'readonly' ] Identifier;
ParameterList ::= Parameter (',' Parameter)*;
ClassDeclaration ::= 'class' Identifier [ 'extends' Identifier ] [ 'implements' Identifier (',' Identifier)* ] Block;
InterfaceDeclaration ::= 'interface' Identifier Block;
EnumDeclaration ::= 'enum' Identifier Block;
TypeAliasDeclaration ::= 'type' Identifier '=' Type;
ImportPath ::= Identifier ('.' Identifier)* [ '.*' | 'as' Identifier | '{' ImportPathList '}' ];
ExportList ::= Identifier [ 'as' Identifier ] (',' Identifier [ 'as' Identifier ])*;
MetadataTerm ::= 'deprecated' | 'experimental' | 'nowarnings' | (gameversion String);

Parameter ::= Identifier ':' Type;
ImportPathList ::= ('self' [ 'as' Identifier ] | ImportPath) (',' ImportPath)*;
```

### 变量声明

变量声明用于声明一个变量，可以使用 `var`、`let` 或 `const` 关键字，分别表示变量、运行时常量和编译时常量。变量声明必须包含一个初始化表达式，变量的类型可以通过类型注解指定，如果没有指定类型，则由编译器根据初始化表达式推断类型。注意：当使用 `let` 或 `const` 声明时，无论是否指定类型注解，或类型注释是否具有 `readonly` 修饰符，编译器都会将该变量视为只读的，例如，当声明的类型为 `Text` 时，该变量的实际类型为 `readonly Text`。

下面是一些变量声明的示例：

```vanillang
var x: int = 10
var y = 0xFF
let name: string = "Vanillang"
const PI: float = 3.14159f
```

### 函数声明

函数声明用于声明一个函数，必须包含一个参数列表，参数列表中的每个参数都必须包含一个类型注解，参数列表可以是空的。函数声明可以选择性地包含一个返回类型注解，如果没有指定返回类型，则由编译器根据函数体中的 `return` 语句推断返回类型，如果函数体中没有 `return` 语句，则返回类型为 `void`。

下面是一些函数声明的示例：

```vanillang
func add(a: int, b: int) -> int {
    return a + b
}

func greet(name: string) {
    print("Hello, " + name + "!")
}
```

### 类型声明

类型声明用于声明一个类型，Vanillang 支持以下几种类型声明：
- 类声明：用于声明一个类，可以包含成员属性和成员方法，可以使用 `extends` 关键字指定一个父类，使用 `implements` 关键字指定一个或多个接口。
- 接口声明：用于声明一个接口，只能包含实例成员方法声明，不能包含实现，Vanillang 不支持接口继承。
- 枚举声明：用于声明一个枚举模式，可以包含一个或多个枚举成员，枚举模式的每个成员都可以有一个或多个关联值，并且在使用时可以通过模式匹配来解构这些关联值。在 Vanillang 中，枚举模式的本质是一个类，其成员为该类的子类。
- 类型别名声明：用于声明一个类型别名，可以将一个类型标识符赋值给另一个类型标识符，表示它们是同一个类型。

下面是一些类型声明的示例：

```vanillang
class Player {
    name: string
    health: int
}

interface Damageable {
    func takeDamage(amount: int) -> void
}

enum Result {
    Success(value: string)
    Failure(error: string)
}

type NamespaceId = string
```

### 属性声明

类成员属性声明用于声明一个类的成员属性，可以使用 `private` 或 `public` 关键字指定访问修饰符，使用 `static` 关键字指定静态属性。类成员属性必须包含一个类型注解，类型注解可以具有 `readonly` 修饰符，表示该属性是只读的。类成员属性可以选择性地包含一个初始化表达式。对于静态属性，若不包含初始化表达式，则会被初始化为该类型的默认值，要求该类型为基本类型或具有无参构造函数；对于实例属性，若不包含初始化表达式，则必须在构造函数中进行初始化，否则编译器会报错。

下面是一些类成员属性声明的示例：

```vanillang
class Player {
    public name: string
    private health: int = 20
    static maxHealth: int = 20
}
```

### 方法声明

类成员方法声明类似于函数声明，用于声明一个类的成员方法，可以使用 `private` 或 `public` 关键字指定访问修饰符，使用 `static` 关键字指定静态方法。类成员方法必须包含一个参数列表，参数列表中的每个参数都必须包含一个类型注解，参数列表可以是空的。类成员方法可以选择性地包含一个返回类型注解，如果没有指定返回类型，则由编译器根据方法体中的 `return` 语句推断返回类型，如果方法体中没有 `return` 语句，则返回类型为 `void`。对于实例方法，方法体内可以使用 `this` 关键字访问当前实例的成员属性和成员方法；对于静态方法，方法体内不能使用 `this` 关键字访问当前实例的成员属性和成员方法，但可以使用类名访问当前类的静态属性和静态方法。

### 模块导入声明

模块导入声明用于导入一个包、模块或标识符，可以使用 `as` 关键字为导入的标识符指定一个别名，或者使用 `*` 导入一个包或模块内的所有导出标识符。同时支持大括号导入，可以在导入时指定要导入的标识符列表，并且可以为每个导入的标识符指定一个别名。

下面是一些模块导入声明的示例：

```vanillang
import vanillang.math
import vanillang.math as m
import vanillang.math.*
import vanillang as vnl
import vanillang.ui.TextDisplayUi
import vanillang.ui.{ TextDisplayUi, Button }
import vanillang.ui.{ self, TextDisplayUi as TDU, Button as Btn }
```

### 模块导出声明

模块导出声明用于导出一个标识符，可以使用 `as` 关键字为导出的标识符指定一个别名，指定别名后，在 `import` 声明中只能使用别名导入该标识符，不能使用原名导入该标识符。

下面是一些模块导出声明的示例：

```vanillang
export Player
export Player as P
export add as sum
export Player, add as sum
```
