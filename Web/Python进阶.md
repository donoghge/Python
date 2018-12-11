## PYthon进阶

#### 1、PEP8

```Python
import sys
import os

from django.conf import settings


def 

''' '''文档，会出现在
#   
```



- 导包：先导系统库， 三方库， 不用*

- 常量大写：
  - 容易导致内存泄漏

- 机器码：
  - 10100101
  - 指令集
- 汇编语言
  - MOV
  - LOOP
  - JMP
  - ADD
- 编译型语言
  - C语言/C++
  - Go



- 解释型语言，脚本语言，动态语言
  - Python
  - Javascript------> V8解释器
  - PHP
  - RUby
  - R



		源代码  Python虚拟机

解释器-------->字节码------------>机器码

- 为什么要有编码规范？

  - 编码是给人看的

  - 美观是重点吗

    1、美观

    2、可读性

    3、可维护性

    4、健壮性

- 代码编排：

  - 缩进4个空格，禁止空格与Tab混用
  - 

zip:得到迭代器

字典无序。

Return a zip object whose .__next__() method returns a tuple where
the i-th element comes from the i-th iterable argument.  The .__next__()
method continues until the shortest iterable in the argument sequence
is exhausted and then it raises StopIteration.



- from aa import *
  - 在使用*导包时， 私有是不能被导入的
  - \_\_all\_\_: 显示暴露在外的参数
- 显式导包：单独导包， 不会受到任何影响



- 解包：



- 默认参数，是保存在函数内部的
- copy,  deepcopy

- pickle: 序列化与反序列化



- 自定义deepcopy：my_deepcopy = lambda item

- 闭包：\_\_closure\_\_

- cell_content

![1543975068120](C:\Users\DELL\AppData\Local\Temp\1543975068120.png)

w:只匹配独立的单词。 vim demo.txt, tank

![1543993178392](C:\Users\DELL\AppData\Local\Temp\1543993178392.png)