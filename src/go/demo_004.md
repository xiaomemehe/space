# 方法
* go没有类，然而可以在结构体类型上定义方法。
* **方法接收者**出现在func关键字和方法名之间的参数中
```
package main
import (
	"fmt"
	"math"
)
type Vertex struct {
	X, Y float64
}
func (v *Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}
func main() {
	v := &Vertex{3, 4}
	fmt.Println(v.Abs())
}

```
* 可以对包中任意的类型定义任意方法，不仅仅是结构体
* 不能对来自其他包的类型或基础类型定义方法。

### 接受者为指针的方法
* 方法可以与 命名类型 或 命名类型的指针 关联
* 使用指针接收者的两个原因：1.避免每个方法调用中拷贝值  2.方法可以修改接收者指向的值

# 接口
* 接口是一组方法定义的集合
* 接口类型的值可以存放实现这些方法的任何值

* 只要实现了该接口中的所有的方法，那么该类就叫做该接口的实现类
```
注意：
1.当需要接口类型的对象时，那么可以使用任意实现类对象代替。
2.接口对象不能访问实现类的属性。
	package main

	import "fmt"
	//定义一个USB接口
	type USB interface {
		start()
		end()
	}
	//实现鼠标类
	type Mouse struct {
		name string
	}

	func (m Mouse) start() {
		fmt.Println(m.name+" - mouse start")
	}
	func (m Mouse) end() {
		fmt.Println(m.name," - mouse end")
	}

	//实现键盘
	type KeyBoard struct {
		name string
	}

	func (k KeyBoard) start() {
		fmt.Println(k.name," - key start")
	}
	func (k KeyBoard) end() {
		fmt.Println(k.name," - key end")
	}

	//
	func testInterface(u USB)  {
		u.start()
		u.end()
	}
	func main() {
		var m = Mouse{"鼠标"}
		var k = KeyBoard{"键盘"}
		testInterface(m)
		testInterface(k)

		var mm  = Mouse{"shshsh"}
		var usb USB
		usb = mm //创建该接口的任意实现类对象昂
		//fmt.Println(usb.name) //不能访问实现类的属性
		usb.start()
		usb.end()
	}


```

# 错误
* Go 程序使用 error 值来表示错误状态
