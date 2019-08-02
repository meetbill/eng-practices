# python 代码格式规范

目前的规范基于 [pep-0008](http://www.python.org/dev/peps/pep-0008/)

<!-- vim-markdown-toc GFM -->

* [1 代码格式](#1-代码格式)
    * [1.1 缩进](#11-缩进)
    * [1.2 行宽](#12-行宽)
    * [1.3 换行](#13-换行)
    * [1.4 引号](#14-引号)
    * [1.5 空行](#15-空行)
    * [1.6 编码](#16-编码)
* [2 import 语句](#2-import-语句)
* [3 空格](#3-空格)
* [4 注释](#4-注释)
    * [4.1 块注释](#41-块注释)
    * [4.2 行注释](#42-行注释)
* [5 docstring](#5-docstring)
    * [5.1 module 注释](#51-module-注释)
    * [5.2 function 注释](#52-function-注释)
    * [5.3 class 注释](#53-class-注释)
* [6 命名规范](#6-命名规范)
* [7 函数返回值](#7-函数返回值)

<!-- vim-markdown-toc -->

## 1 代码格式
### 1.1 缩进

使用 4 个空格进行缩进

### 1.2 行宽

每行代码尽量不超过 80 个字符

理由：

* 这在查看 side-by-side 的 diff 时很有帮助
* 方便在控制台下查看代码
* 太长可能是设计有缺陷

### 1.3 换行

Python 支持括号内的换行。这时有两种情况。

1) 第二行缩进到括号的起始处

```python
foo = long_function_name(var_one, var_two,
                         var_three, var_four)
```

2) 第二行缩进 4 个空格，适用于起始括号就换行的情形

```python
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)
```

使用反斜杠`\`换行，二元运算符`+` `.`等应出现在行末；长字符串也可以用此法换行

```python
session.query(MyTable).\
        filter_by(id=1).\
        one()

print 'Hello, '\
      '%s %s!' %\
      ('Harry', 'Potter')
```

禁止复合语句，即一行中包含多个语句：

```python
# yes
do_first()
do_second()
do_third()

# no
do_first();do_second();do_third();
```

`if/for/while`一定要换行：

```python
# yes
if foo == 'blah':
    do_blah_thing()

# no
if foo == 'blah': do_blash_thing()
```

### 1.4 引号

简单说，自然语言使用双引号，机器标示使用单引号，因此 __代码里__ 多数应该使用 __单引号__

 * ***自然语言*** **使用双引号** `"..."`
   例如错误信息；很多情况还是 unicode，使用`u"你好世界"`
 * ***机器标识*** **使用单引号** `'...'`
   例如 dict 里的 key
 * ***正则表达式*** **使用原生的双引号** `r"..."`
 * ***文档字符*** **使用三个双引号** `"""......"""`

### 1.5 空行
* 模块级函数和类定义之间空两行；
* 类成员函数之间空一行；

```python
class A:

    def __init__(self):
        pass

    def hello(self):
        pass


def main():
    pass
```

* 可以使用多个空行分隔多组相关的函数
* 函数中可以使用空行分隔出逻辑相关的代码

### 1.6 编码

* 文件使用 UTF-8 编码
* 文件头部加入`#-*-conding:utf-8-*-`标识

## 2 import 语句

> import 语句应该分行书写

```python
# yes
import os
import sys

# no
import sys,os

# yes
from subprocess import Popen, PIPE
```

> 『建议』 [PY002] 禁止使用 from xxx import *

> 『建议』 [PY003] import 时必须使用 package 全路径名（相对 PYTHONPATH)，禁止使用相对路径（相对当前路径），禁止使用 sys.path.append('../../') 等类似操作改变当前环境变量。

避免模块名冲突，查找包更容易。部署时保持项目结构，使用 virtualenv 等创建隔离的 Python 环境，并配置需要的 PYTHONPATH。
```python
# yes
from foo.bar import Bar

# no
from ..bar import Bar
```

> import 语句应该放在文件头部，置于模块说明及 docstring 之后，于全局变量之前；

> import 语句应该按照顺序排列，每组之间用空行分隔

```python
import os
import sys

import msgpack
import zmq

import foo
```

> 『建议』 禁止使用 from xxx import yyy 语法直接导入类或函数（即 yyy 只能是 module 或 package，不能是类或函数）。

```
避免冲突。调用关系简单明了，x.obj 表示 obj 对象定义在模块 x 中。

#YES
from Crypto.Cipher import AES
import os
os.unlink(path)

#NO
# os 已经是最底下的模块了
from os import unlink
unlink(path)
```
## 3 空格
* 在二元运算符两边各空一格`[=,-,+=,==,>,in,is not, and]`:

```python
# yes
i = i + 1
submitted += 1
x = x * 2 - 1
hypot2 = x * x + y * y
c = (a + b) * (a - b)

# no
i=i+1
submitted +=1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)
```

* 函数的参数列表中，`,`之后要有空格

```python
# yes
def complex(real, imag):
    pass

# no
def complex(real,imag):
    pass
```

* 函数的参数列表中，默认值等号两边不要添加空格

```python
# yes
def complex(real, imag=0.0):
    pass

# no
def complex(real, imag = 0.0):
    pass
```

* 左括号之后，右括号之前不要加多余的空格

```python
# yes
spam(ham[1], {eggs: 2})

# no
spam( ham[1], { eggs : 2 } )
```

* 字典对象的左括号之前不要多余的空格

```python
# yes
dict['key'] = list[index]

# no
dict ['key'] = list [index]
```

* 不要为对齐赋值语句而使用的额外空格

```python
# yes
x = 1
y = 2
long_variable = 3

# no
x             = 1
y             = 2
long_variable = 3
```

## 4 注释
### 4.1 块注释
"#" 号后空一格，段落件用空行分开（同样需要“#”号）
```python
# 块注释
# 块注释
#
# 块注释
# 块注释
```

### 4.2 行注释
至少使用两个空格和语句分开，使用有意义的注释
```python
# yes
x = x + 1  # 边框加粗一个像素

# no
x = x + 1 # x 加 1
```

## 5 docstring
docstring 的规范在 [PEP 257](http://www.python.org/dev/peps/pep-0257/) 中有详细描述，其中最其本的两点：

> * 1. 所有的公共模块、函数、类、方法，都应该写 docstring。私有方法不一定需要，但应该在 def 后提供一个块注释来说明。
> * 2.docstring 的结束"""应该独占一行，除非此 docstring 只有一行。
> * 3·『强制』使用 docstring 描述 module、function、class 和 method 接口。docstring 必须用三个双引号括起来。
> * 4·『强制』对外接口部分必须用 docstring 描述，内部接口视情况自行决定是否写 docstring。
> * 5·『强制』接口的 docstring 描述至少包括功能简介、参数、返回值。如果可能抛出异常，必须注明。
> * 6·『强制』每个文件都必须有文件声明，文件声明必须包括以下信息：版权声明，功能和用途简介，修改人及联系方式。
> * 7·『建议』TODO 注释格式必须为：
>   * # TODO: 干什么事情 $ 负责人（邮箱前缀）$ 最终期限 (YYYY-MM-DD)$

```python
"""Return a foobar
Optional plotz says to frobnicate the bizbaz first.
"""

"""Oneline docstring"""
```
### 5.1 module 注释

```
Authors:
Date: 2019/04/05 17:23:06
```

### 5.2 function 注释

```
Args:
    ...
Returns:
    ...
example:
    ...
Raises:
    ...
```

### 5.3 class 注释

```
Attributes:
    ...
```

## 6 命名规范

* 应避免使用小写字母 l(L)，大写字母 O(o) 或 I(i) 单独作为一个变量的名称，以区分数字 1 和 0
* 包和模块使用全小写命名，尽量不要使用下划线
* 类名使用 CamelCase 命名风格，内部类可用一个下划线开头
* 函数使用下划线分隔的小写命名
* 当参数名称和 Python 保留字冲突，可在最后添加一个下划线，而不是使用缩写或自造的词
* 常量使用以下划线分隔的大写命名
* '_'单下划线开头：弱“内部使用”标识，如：”from M import *”，将不导入所有以下划线开头的对象，包括包、模块、成员 , 单下划线结尾_：只是为了避免与 python 关键字的命名冲突
* '__'双下划线开头：模块内的成员，表示私有成员，外部无法直接调用

```python
MAX_OVERFLOW = 100

Class FooBar:

    def foo_bar(self, print_):
        print(print_)
```

## 7 函数返回值

每个函数应该有足够明确的语义，基于函数值得语义，函数返回值有 3 种类型

> * True,False
>   * "逻辑判断型" 的函数，表示真或假，如：`is_white_cat()`
> * OK,ERROR
>   * "操作型" 的函数，表示成功或失败，如：data_get()
> * Data,None
>   * "获取数据型" 的函数，表示 "有数据" 或者 "无数据 / 获取失败"，如 data_get()

