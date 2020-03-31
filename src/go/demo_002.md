# for
* 格式：for ;; {} 不能使用 ()
* for i<10 {} //类似while(i<10) go中没有while
* for {}  死循环

# if
* 格式：if statement {}
* if的便捷语句： if语句可以在条件执行前执行一个简单的语句，如 :if a:=1;a==1 {}

# switch
* 不用break
```
package main
import (
	"fmt"
	"runtime"
)
func main() {
	fmt.Print("Go runs on ")
	switch os := runtime.GOOS; os {
		case "darwin":
			fmt.Println("OS X.")
		case "linux":
			fmt.Println("Linux.")
		default:
			// freebsd, openbsd,
			// plan9, windows...
			fmt.Printf("%s.", os)
	}
}
```
* 没有条件的switch，同 switch true 一样，可以以更清晰的形式编写长的if-then-else结构

# defer
* defer语句会延迟函数的执行，直到上层函数返回
* 延迟调用的参数会立刻生成，但是在上层函数返回前函数都不会被调用
* 延迟调用的函数被压入一个栈中。
* 调用顺序为：后进先出
* 
