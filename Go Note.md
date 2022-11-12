# Go 学习笔记
#### Go语言基本特点（引入）
示例代码：
```go
package main 
import "fmt"// 我们需要使用fmt包中的Println()函数
func main() { 
fmt.Println("Hello, world. 你好，世界！") 
} 
```
>每个Go源代码文件的开头都是一个package声明，表示该Go代码所属的包。


>要生成Go可执行程序，必须建立一个名字为main的包，并且在该包中包含一个叫main()的函数（该函数是Go可执行程序的执行起点）


>在包声明之后，是一系列的import语句，用于导入该程序所依赖的包。由于本示例程序用
到了Println()函数，所以需要导入该函数所属的fmt包。

Go语言函数定义的格式为
```go
func 函数名(参数列表)(返回值列表) { 
 // 函数体
} 
```

对应实例：
```go
func Compute(value1 int, value2 float64)(result float64, err error) { 
 // 函数体
} 
```
Go支持多个返回值。以上的示例函数Compute()返回了两个值，一个叫result，另一个是
err。并不是所有返回值都必须赋值。在函数返回时没有被明确赋值的返回值都会被设置为默认
值，比如result会被设为0.0，err会被设为nil。
代码注释的格式与C++是一样的。
**但是Go代码摒弃了C++每步之后都加上分号的习惯，并且Go中规定不可把花括号{放置于另一行**

编译运行go程序前需要使用**go run + 文件名**的指令。
***
## 变量
### 定义
Go语言引入了关键字var，而类型信息放在变量名之后，示例如下：
```go
var v1 int
var v2 string
var v3 [10]int // 数组
var v4 []int // 数组切片
var v5 struct { 
 f int
} 
var v6 *int // 指针
var v7 map[string]int // map，key为string类型，value为int类型
var v8 func(a int) int
```
var关键字的另一种用法是可以将若干个需要声明的变量放置在一起，免得程序员需要重复
写var关键字，如下所示：
```go
var ( 
 v1 int
 v2 string
)
```
### 初始化
对于声明变量时需要进行初始化的场景，var关键字可以保留，但不再是必要的元素，如下
所示：
```go
var v1 int = 10  
var v2 = 10 
v3 := 10 
```
以上声明都是正确的，**相当于能够自动判断数据类型**。其中Go中的C++没有的符号:=同时实现了变量声明和初始化的工作。

当然，出现在:=左侧的变量不应该是已经被声明过的，否则会导致编译错误，比如下面这个
写法：
```go
var i int 
i := 2 
```
会导致类似如下的编译错误：
no new variables on left side of := 
### 赋值
#### Go语法的独特优势
##### 多重赋值
比如交换i跟j的值，只需要引入中间变量t即可：
```go
t = i; i = j; j = t; 
```
##### 匿名变量
利用该语法可省略定义许多无用变量，如：
```go
func GetName() (firstName, lastName, nickName string) { 
 return "May", "Chan", "Chibi Maruko" 
} 
```
若只想获得nickName，则函数调用语句可以用如下方式编写：
```go
_, _, nickName := GetName() 
```
***
## 常量
#### 字面常量
字面常量，是指程序中硬编码的常量，如：
-12 
3.14159265358979323846 // 浮点类型的常量
3.2+12i // 复数类型的常量
true // 布尔类型的常量
"foo" // 字符串常量


Go语言的字面常量是无类型的。只要这个常量在相应类型的值域范围内，就可以作为该类型的常量，比如-12，它可以赋值给int、uint、int32、int64、float32、float64、complex64、complex128等类型的变量。
### 定义
#### 常量定义
利用const关键字进行定义，如：
```go
const Pi float64 = 3.14159265358979323846 
const zero = 0.0 
const (
 size int64 = 1024 
 eof = -1 
)//该定义方法与变量相似
const u, v float32 = 0, 3 // u = 0.0, v = 3.0，常量的多重赋值
const a, b, c = 3, 4, "foo" 
```
#### 预定义常量
iota——会根据语法被编译自动修改的量


规则：在每一个const关键字出现时被重置为0，然后在下一个const出现之前，每出现一次iota，其所代表的数字会自动增1。
### 枚举
其本质类似于定义一组常量时常量值的传递并递增，如：
```go
const ( 
 Sunday = iota
 Monday 
 Tuesday 
 Wednesday 
 Thursday 
 Friday 
 Saturday 
 numberOfDays // 这个常量没有导出 
)
```
### 类型
Go语言内置以下这些基础类型：
1.布尔类型：bool。
2.整型：int8、byte、int16、int、uint、uintptr等。
3.浮点类型：float32、float64。
4.复数类型：complex64、complex128。
5.字符串：string。
6.字符类型：rune。
7.错误类型：error。
此外，Go语言也支持以下这些复合类型：
1.指针（pointer）
2.数组（array）
3.切片（slice）
4.字典（map）
5.通道（chan）
6.结构体（struct）
7.接口（interface）
##### 布尔类型