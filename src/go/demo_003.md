# 指针
* go具有指针，指针保存了变量的内存地址
* 类型 \*T是指向T类型的指针。零值为 nil
* 定义：var p \*int
* &符号会生成一个指针，指向其作用对象：i := 1   p = &i
* 间接引用，可以通过指针设置变量
```
package main
import "fmt"
func main() {
	a := 1
	i := &a
	*i = 3
	fmt.Println(a)//3
}
```

# 结构体 struct
* 结构体是一个集合，字段的集合
* 结构体字段通过点好来访问
* 结构体字段可以通过结构体指针来访问(或赋值修改)，通过指针的间接访问时透明的
* 结构体文法表示通过结构体的字段的值，为列表来新分配一个结构体
* 使用 Name : 语法可以仅列出部分字段，特殊的 & 符号返回一个指向结构体的指针
```
type Vertex struct {
	X, Y int
}
var (
	v1 = Vertex{1, 2}  // 类型为 Vertex
	v2 = Vertex{X: 1}  // Y:0 被省略
	v3 = Vertex{}      // X:0 和 Y:0
	p  = &Vertex{1, 2} // 类型为 *Vertex
)
func main() {
	fmt.Println(v1, p, v2, v3)
}

```

# 数组
* 定义：[n]T  n个类型为T的值的数组，var a [3]int
* 数组的长度是其类型的一部分，因此不能改变数组的大小

# slice
* 一个slice会指向一个序列的值，并且包含了长度信息
* []T 是一个元素类型为T的slice
* slice可以重新切片，表达式为：[lo:hi],表示 从lo 到 hi-1 的slice元素，含两端。  s[lo:lo] 为空，s[lo:lo+1] 有一个元素
* slice由函数make创建。这会分配一个零长度的数组并且返回一个slice指向这个数组。 a := make([],5) //[0,0,0,0,0]
* 容量：make([]int,0,5)//第三个参数为指定的容量
```
b := make([]int, 0, 5) // len(b)=0, cap(b)=5   []
b = b[:cap(b)] // len(b)=5, cap(b)=5   [0,0,0,0,0]
b = b[1:]      // len(b)=4, cap(b)=4	[0,0,0,0]
```
* slice 零值为 nil  一个nil 的slice 的长度和容量 为 0
* 添加元素：append(s []T,vs ...T) []T  //s 为类型为T的数组
* 如果s底层数组太小，而不能容纳所有值时，会分配一个更大的数组。返回的slice会指向新的数组

# range
* for需要的range格式可以对slice 和 map进行迭代循环。
* 可以通过 \_ 来忽略序号和值，如： for \_,value := range(list) {}

# map映射键到值
* map使用前必须用make  而不是 new 来创建。 值为nil 的map是空的，且不能赋值
* map的文法和 struct结构体的文法类似，不过必须有键名
```
package main
import "fmt"
type Vertex struct {
	Lat, Long float64
}
var m = map[string]Vertex{
	"Bell Labs": Vertex{//这里的Vertex 可以省略
		40.68433, -74.39967,
	},
	"Google": Vertex{
		37.42202, -122.08408,
	},
}

func main() {
	fmt.Println(m)
}

如果顶级的类型只有类型名的话，可以在文法的元素中省略键名

```
* 修改、新增map  m[key] = value, 删除 delete(m[key])
* 通过双赋值检测某个键是否存在： elem,ok := m[key]  //存在，ok为true时，否则，ok为false，并且为false是，elem为元素的零值
* 当读取map中不存在的键是，结果为元素的零值 。 如：m["NNN"] = {0,0}

# 函数
* 函数也是值
* GO函数可以是闭包的。闭包是一个函数值，它来自函数体的外部的变量引用。函数可以对这个引用值进行访问和赋值；换句话说，这个函数被绑定在了变量上。
* 
