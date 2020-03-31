# 包
* 每个go程序都是由包package组成的。程序入口为main
* 按照惯例，包名与导入路径的最后一个目录一致。例如：import "math/rand" 包由 package rand 语句开始
```
 import (
	"fmt"
	"math/rand"
 	)
 和
 import "fmt"
 import "math/rand"
 效果一致
```
* Go中，首字母大写的名称是被导出的。例如 ：Foo、FOO都是可以被导出的，foo不可以

# 函数
* 函数可以没有参数，或者接受多个参数
* 形参：类型在变量名之后 如 func demo(a int,b string) void {}
* 两个或多个连续的函数命名参数类型一致，可以只保留最后一个类型,如 func demo (a string,b,c,d int) void {}
* 函数返回值：可以是多个
* 没有参数的返回值，如只是 return ,返回结果的当前值.如
```
func test(a int, b int) (aa int) {
	aa = a*b
	return
}

test(2,3) //6
```

# 变量
* 定义：var x,y int
* 可以定义在包或函数级别
* 初始值：var x,y int = 1,2 (int可以省略)  如果初始化使用的是表达式 可以省略类型  如 var z = x +y
* :=,简洁赋值语句，可以用于代替 var 方式，注意**不能使用在函数外，函数外必须以var关键字开头**
* 变量在定义时未初始化，默认赋值 零值。 如：数值类型为0 ， 布尔类型为 false  字符串类型为 ”“
* 类型转换:格式-> T(v)
* 类型推导：右侧指定了类型，左侧和右侧类型一致，右侧未指定类型，取决于右侧精度

# 常量
* 关键字const，可以是字符，字符串，布尔或数字类型的值
* 常量不能使用 := 语法定义
* 一个未指定类型的常量由上下文来决定其类型

# Go的基本类型
* bool
* string
* int int8 int16 int32 int64
* uint uint8 uint16 uint32 uint64 **uintptr**
* byte uint8的别名
* rune int32的别名，代表一个Unicode码
* float32 float64
* complex64 complex128
