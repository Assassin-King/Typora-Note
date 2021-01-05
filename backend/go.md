

# 目录

[toc]

## 基础语法

### var 和 :=

```go

//定义变量并初始化值
var number1, number2, number3 int = 1, 2, 3

//忽视声明类型
var number1, number2, number3 = 1, 2, 3

//:= 再度简化。不过只能用在函数内部；在函数外部使用则会无法编译通过，所以一般用var方式来定义全局变量。
number1, number2, number3 := 1, 2, 3
```



### 数组

```go
var arr1 [5]int
for i:=0; i < len(arr1); i++ {
        arr1[i] = i * 2
    }
```

```go
var a = [10]int{1,2,3,4,5,6,7,8,9,0}

//不足自动补0
var a = [10]int{1,2,3,4}　　　　　　　　　　　　　　　　

//如果忽略 [] 中的数字不设置数组大小，Go 语言会根据元素的个数来设置数组的大小：
var a = [...]int{1,2,3,4,5}
```

```go
//遍历
var a = [...]int{1, 2, 3, 4, 5}

func bianli1() {
	for _, e := range a {
		fmt.Println(e)
	}
}

func bianli2() {
	for i := 0; i < len(a); i++ {
		fmt.Println(a[i])
	}
}

```

### 切片

```go
//通过 make() 函数创建切片
slice := make([]int, 5)       //其长度和容量都是 5 个元素
slice := make([]int, 3, 5)    //其长度为 3 个元素，容量为 5 个元素

//通过字面量创建切片,和创建数组类似，只是不需要指定[]运算符里的值
myStr := []string{"aa", "bb", "cc"}  // 其长度和容量都是 3 个元素
myStr := []string{99: ""}  // 使用空字符串初始化第 100 个元素


// 创建有 3 个元素的整型数组
myArray := [3]int{10, 20, 30}
// 创建长度和容量都是 3 的整型切片
mySlice := []int{10, 20, 30}
```



```go
func sliceTest() {
	slice := []string{"11", "bobo", "22", "333"}
	s := []string{}
	s = append(slice, "fsd")
	fmt.Println(s)
	slice2 := slice[1:3]
	fmt.Println(slice2)

	// 取左不取右
	//[11 bobo 22 333 fsd]
	//[bobo 22]
}

```

### Map (无序的键值对的集合)

```go
    m := map[string]int{"one": 1, "two": 2}
	m["three"] = 3
	fmt.Println(m)  // map[one:1 three:3 two:2]

	// 删除key 为one 的元素
	delete(m, "one")
	fmt.Println(m)   //map[three:3 two:2]

	//清空map 元素
    m = nil 
	fmt.Println(m, len(m))  //map[] 0
```

```go
//比较两个map
package main
import (
   "fmt"
   "reflect"
)
func main() {
   m1 := map[string]int{"a": 1, "b": 2, "c": 3}
   m2 := map[string]int{"a": 1, "c": 3, "b": 2}
   //方法一
   fmt.Println(reflect.DeepEqual(m1, m2))
   //方法二
   fmt.Println(cmpMap(m1, m2))
}
func cmpMap(m1, m2 map[string]int) bool {
   if len(m1) == len(m2) {
      for k1, v1 := range m1 {
         if v2, ok := m2[k1]; ok {
            if v1 != v2 {
               return false
            }
         } else {
            return false
         }
      }
      return true
   }
   return false
}
```



### struct

数组只能存放单一的数据类型，可以将不同类型的数据存放到struct。在GO中没有class的关键字，但GO是通过struct结构与method方法组合来实现的面向对象。

```go
type Person struct {
	Name string
	Age  int
}
```

```go
func main() {
	a := Person{}
	a.Age = 12
	a.Name = "bobo"
	fmt.Println(a)  //{bobo 12}
}

```

```go
//struct 作为一种类型和其他类型结合用
func main() {
	m := map[string]Person{}
	p := Person{Name: "aa", Age: 22}
	m["test"] = p
	fmt.Println(m)  //map[test:{aa 22}]
}

```

```go
//struct 面向对象示例
func main() {
	p := Person{Name: "aa", Age: 22}
	p.list()
}

func (p *Person) list() {
	fmt.Println(p.Age)  //22
}
```



### 匿名字段

定义一个struct，定义的时候是字段名与其类型一一对应，实际上Go语言支持只提供类型，而不写字段名的方式，也就是匿名字段，或称为嵌入字段。

### OK 断言

ok即断言，可以断言某一个变量是特定类型，也可以断言map中存在某一个key值

```go
    
    var v interface{} = 1
	v1, ok := v.(int)
	fmt.Println(v1, ok) //1 true

	v2, ok := v.(string) //  false
	fmt.Println(v2, ok)

	v3, ok := v.(bool)
	fmt.Println(v3, ok) //false false

	m := map[string]int{"one": 1, "two": 2}
	v4, ok := m["two"]
	fmt.Println(v4, ok) //2 true

	v5, ok := m["2222"]
	fmt.Println(v5, ok) //0 false
```

### 逗号OK 模式



## 单元测试 (go test -v)

###  示例

创建目录test，在目录下创建add.go、add_test.go两个文件，add_test.go为单元测试文件。

```go
// add_test.go

package test
import "testing"
func TestAdd(t *testing.T) {
   sum := Add(1, 2)
   if sum == 3 {
      t.Log("the result is ok")
   } else {
      t.Fatal("the result is wrong")
   }
}
func TestAdd1(t *testing.T) {
    t.Error("the result is error")
}
```

```go
// add.go

package test
func Add(a, b int) int {
   return a + b
}
```

```go
// 然后在项目目录下运行go test -v就可以看到测试结果了

=== RUN   TestAdd
--- PASS: TestAdd (0.00s)
    add_test.go:8: the result is ok
=== RUN   TestAdd1
--- FAIL: TestAdd1 (0.00s)
    add_test.go:14: the result is error
FAIL
exit status 1
FAIL    _/D_/gopath/src/ados/test       0.419s
```

### 规则

使用testing库的测试框架需要遵循以下几个规则如下：

- 文件名必须是`_test.go`结尾的，这样在执行`go test`的时候才会执行到相应的代码
- 你必须import `testing`这个包
- 所有的测试用例函数必须是`Test`开头
- 测试用例会按照源代码中写的顺序依次执行
- 测试函数`TestXxx()`的参数是`testing.T`，我们可以使用该类型来记录错误或者是测试状态
- 测试格式：`func TestXxx (t *testing.T)`,`Xxx`部分可以为任意的字母数字的组合，但是首字母不能是小写字母[a-z]，例如`Testintdiv`是错误的函数名。
- 函数中通过调用`testing.T`的`Error`, `Errorf`, `FailNow`, `Fatal`, `FatalIf`方法，说明测试不通过，调用`Log`方法用来记录测试的信息。

## 报错整理

### go: cannot find main module

```go
cd进入项目目录

输入go mod init

或在上层目录输入go mod init project_name
```

### expected 'package', found 'EOF'

```go
文件保存下重新运行
```



## 开发工具

### VsCode

#### 代码补全提示

```go
    // settings.json 文件添加
    "go.useCodeSnippetsOnFunctionSuggest": true,
    "go.useLanguageServer": true,
    "go.goroot": "",
    "go.gopath": "",
    "go.inferGopath": true,
    "go.autocompleteUnimportedPackages": true,
    "go.gocodePackageLookupMode": "go",
    "go.gotoSymbol.includeImports": true,
    "go.useCodeSnippetsOnFunctionSuggestWithoutType": true,
    "go.alternateTools": {
        
    },
    "editor.quickSuggestionsDelay": 1
```

