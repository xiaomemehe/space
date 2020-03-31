# goroutine
* goroutine是go运行时环境管理的轻量级线程 ： go f(x,y,z)
* 开启一个新的goroutine执行：f(x,y,z)

# channel
* channel是有类型的管道，可以用channel操作符 <- 对其发送或接受值
* ch <- v  //将v送入channel ch
* v := <-ch //从ch接收，并赋值给v
* 和map与slice一样，channel使用前必须创建：
* ch := make(chan int)
* 默认情况下，在另一端准备好之前，发送和接收都会阻塞。这使得goroutine可以在没有明确的锁或竞争变量的情况下进行同步。
###  缓冲channel
* channel可以是 _ 带缓冲的_  为make提供第二个参数作为缓冲长度来初始化一个缓冲channel：
* ch := make(chan int, 100)
* 向缓冲channel发送数据的时候，只有在缓冲区满的时候才会阻塞	。当缓冲区清空的时候接受阻塞。

### range和close、select
* 发送者可以close一个channel来表示再没有值会被发送了。接收者可以通过赋值语句的第二个参数来测试channel是否被关闭:当没有值可以接收并且channel已经被关闭，那么经过：v,ok := <-ch 之后 ok 会被设置为‘false’

* 上代码
```
func main() {
    ch := make(chan int,1)
    for i := 0; i < 10; i++{
        select {
        case ch <- i:
        case x := <- ch:
            fmt.Println(x)
        }
    }
}

0
2
4
6
8
```
* why
* 管道缓冲大小为1,第一遍 i=0 时走的是 ch<-i 将 0 写入管道中，i=1时，管道中有数据，走的是x := <- ch。依次
