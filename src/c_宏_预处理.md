# C_宏_预处理.md

### 定义
* **#define**叫做***宏定义命令***,它也是C语言预处理命令的一种。
* 所谓宏定义，就是用一个标识符来表示一个字符串，如果在后面的代码中出现该标识符，那么就全部替换成指定的字符串。

```

宏定义的一般形式为：
	#define 宏名 字符串
1. #表示这是一条预处理命令，所有的预处理命令都是以#开头。
2. 宏名是标识符的一种，命名规则和变量相同。
3. 字符串可以是数字、表达式、if 语句、函数等。

对于#define用法的几点说明：
1. 宏定义是用宏名表示一个字符串，在宏展开时以该字符串替换宏名，这只是简单的替换，预处理程序对他不做任何检查，如有错误，只能编译已被宏展开后的源程序时发现。
2. 宏定义不是说明或语句，行末不用加分号，分号会被一起带入替换。
3. 宏定义必须写在函数外面，作用域为定义起到源程序结束。如要终止其作用域，可使用#undef
4. 代码中的宏名如果被引号包含，预处理程序不对其做替换
5. 宏定义允许嵌套，在宏定义的字符串中可以使用已经定义过的宏名
6. 习惯用大写字母，小写字母也可以。
7. 可以用宏定义表示数据类型，如:
* #define UINT unsigned int
```

### 带参数的宏定义

```

* 带参宏定义的一般形式为：
#define 宏名(形参列表) 字符串
* 调用方式
宏名(实参列表);

1. 宏名和形参列表之间不能有空格
2. 在带参宏中，不会为形参分配内存，因此不必指明数据类型。而实参包含具体数据，需要指明类型
**（这一点和函数是不同的：在函数中，形参和实参是两个不同的变量，都有自己的作用域，调用时要把实参的值传递给形参；而在带参数的宏中，只是符号的替换，不存在值传递的问题。）**
3. 在宏定义中，字符串内的形参通常用括号包含，避免出错，如:
x*x  如果 x 被替换为 y+1  如果不用括号包含，为y+1*y+1


```
