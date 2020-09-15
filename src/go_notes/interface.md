```
package main

import (
	"fmt"
)

type People interface {
	Speak(string) string
}

type Student struct{}

//除了指针不能接受非指针对象，其他都可以
func (stu *Student) Speak(think string) (talk string) {
	if think == "sb" {
		talk = "你是个大帅比"
	} else {
		talk = "您好"
	}
	return
}

func main() {
	var peo People = Student{} //这里需要 &Student{}
	think := "sb"
	fmt.Println(peo.Speak(think))
}
```

from <a href="http://www.topgoer.com/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1/%E6%8E%A5%E5%8F%A3.html">link</a>
