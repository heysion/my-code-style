# 头文件

##  #define 保护

命名格式当是: <PROJECT>_<PATH>_<FILE>_H_

为保证唯一性, 头文件的命名应该依据所在项目源代码树的全路径. 例如, 项目 foo 中的头文件 foo/src/bar/baz.h 可按如下方式保护:

    #ifndef FOO_BAR_BAZ_H_
    #define FOO_BAR_BAZ_H_
    …
    #endif // FOO_BAR_BAZ_H_

## 头文件依赖

能用前置声明的地方尽量不使用 #include.


## 内联函数

只有当函数只有 10 行甚至更少时才将其定义为内联函数.

    定义:当函数被声明为内联函数之后, 编译器会将其内联展开, 而不是按通常的函数调用机制进行调用.
    优点:当函数体比较小的时候, 内联该函数可以令目标代码更加高效. 对于存取函数以及其它函数体比较短, 性能关键的函数, 鼓励使用内联.
    缺点:滥用内联将导致程序变慢. 内联可能使目标代码量或增或减, 这取决于内联函数的大小. 内联非常短小的存取函数通常会减少代码大小, 但内联一个相当大的函数将戏剧性的增加代码大小. 现代处理器由于更好的利用了指令缓存, 小巧的代码往往执行更快。
    结论:一个较为合理的经验准则是, 不要内联超过 10 行的函数. 谨慎对待析构函数, 析构函数往往比其表面看起来要更长, 因为有隐含的成员和基类析构函数被调用!
    
    另一个实用的经验准则: 内联那些包含循环或 switch 语句的函数常常是得不偿失 (除非在大多数情况下, 这些循环或 switch 语句从不被执行).
    
    有些函数即使声明为内联的也不一定会被编译器内联, 这点很重要; 比如虚函数和递归函数就不会被正常内联. 通常, 递归函数不应该声明成内联函数.（YuleFox 注: 递归调用堆栈的展开并不像循环那么简单, 比如递归层数在编译时可能是未知的, 大多数编译器都不支持内联递归函数). 虚函数内联的主要原因则是想把它的函数体放在类定义内, 为了图个方便, 抑或是当作文档描述其行为, 比如精短的存取函数.
    

# 命名约定

函数命名, 变量命名, 文件命名应具备描述性; 不要过度缩写. 类型和变量应该是名词, 函数名可以用 “命令性” 动词.


尽可能给出描述性的名称. 不要节约行空间, 让别人很快理解你的代码更重要.

好的命名风格:

    int num_errors;                  // Good.
    int num_completed_connections;   // Good.


## 文件命名

文件名要全部小写, 可以包含下划线 (_) 或连字符 (-). 按项目约定来.

可接受的文件命名:

    my_useful_class.c
    my-useful-class.c
    myusefulclass.c

## 类型命名

类型名称的每个单词首字母均大写, 不包含下划线: MyExcitingClass, MyExcitingEnum.

所有类型命名 —— 类, 结构体, 类型定义 (typedef), 枚举 —— 均使用相同约定. 例如:

    // classes and structs
    class UrlTable { ...
    class UrlTableTester { ...
    struct UrlTableProperties { ...
    
    // typedefs
    typedef hash_map<UrlTableProperties *, string> PropertiesMap;
    
    // enums
    enum UrlTableErrors { ...}}}}


## 变量命名

变量名一律小写, 单词之间用下划线连接. 类的成员变量以下划线结尾, 如:

    my_exciting_local_variable
    my_exciting_member_variable_

全局变量:

    对全局变量没有特别要求, 少用就好, 但如果你要用, 可以用 g_ 或其它标志作为前缀, 以便更好的区分局部变量.

常量命名:

在名称前加 k: kDaysInAWeek.

所有编译时常量, 无论是局部的, 全局的还是类中的, 和其他变量稍微区别一下. k 后接大写字母开头的单词::

const int kDaysInAWeek = 7;

## 函数命名

常规函数使用大小写混合, 取值和设值函数则要求与变量名匹配:

    MyExcitingFunction(), MyExcitingMethod(), my_exciting_member_variable(), set_my_exciting_member_variable().

常规函数:

函数名的每个单词首字母大写, 没有下划线:

    AddTableEntry()
    DeleteUrl()

## 命名规则的特例

如果你命名的实体与已有 C/C++ 实体相似, 可参考现有命名策略.


bigopen():  函数名, 参照 open() 的形式

uint: typedef

bigpos: struct 或 class, 参照 pos 的形式

sparse_hash_map: STL 相似实体; 参照 STL 命名约定

LONGLONG_MAX:    常量, 如同 INT_MAX 

