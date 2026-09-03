# Vanillang 包

Vanillang 的包是一个目录，该目录下可能包含一个或多个模块或子包，编译器在编译时，会将 `config` 中的 `packageRootPath` 的 `filename` 作为根包的包名，并将该目录下的所有源文件编译为该包的成员。包的命名必须满足标识符的命名规则。