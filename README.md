# Compiler

## 项目要求

*编译器演示程序，可将C 语言测试程序编译为目标代码——汇编程序，用汇编器转换为二进制程序后运行无误。*

1. 基本要求

    * 数据类型：int

    * 语句：注释，声明，赋值，循环（while和for）判断（if），输入输出

    * 算术运算：+，-，*，/，%，^

    * 关系运算：==，>，<，>=，<=，!=

    * 逻辑运算：&&（与），||（或），!（非）


## 环境准备

* 操作系统：**Ubuntu LTS 18.04**，或者其他的**GNU LINUX**发行版

* 依赖包：`nasm`，`flex`，`bison`，`gcc-multilib`，`build-essential`

## 如何运行

* 在代码根目录执行`make grammar`

* 在代码根目录执行`make`

* 执行`make build`

* `cd build`，然后执行`make`

* 运行文件生成的二进制文件

## 文件目录说明

1. `common`目录

    包含了主要类文件，目录下的trees.h文件包含了与语法树相关的类，外部使用时只需要包含该头文件即可包含所有相关头文件

    * `symbol`子目录

        包含了symbol符号表类、FuncSymbol符号表类的源文件

    * `trees`子目录

        包含了抽象语法树（AST）相关类源文件
    
    * `util`子目录

        包含主要工具类，中间代码类、汇编代码生成类、io汇编源文件

2. `Linux`/`MacOS`


3. `Makefile`，Linux系统的构建文件

## 相关代码说明

1. `./common/symbol/symbol.h`中`SymbolTable`类的说明

    |类方法|返回值|参数列表|作用|参数意义|
    |:----:|:---:|:-----:|:--:|:-----:|
    |`SymbolTable`||`bool isFun`|唯一公有构造函数，创建一个空的符号表|该作用域是否为函数|
    |`createChildTable`|`SymbolTable*`|`bool isFun`|创建一个子符号表并返回（已经设置了peer指针和child指针，调用者无需负责）|该子符号表控制作用域是否为函数|
    |`addSymbol`|`int`|`string idName, symbolType idType`|尝试向当前符号表添加符号，如果存在相同符号名返回-1，成功则返回0|符号名和符号类型|
    |`findSymbol`|`symbol*`|`const string name`|在符号表中搜索符号，如果当前符号表没有搜索到则向父级符号表搜索|符号名|

