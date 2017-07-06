之前在reflect的tyoeof()方法上耗去了大量的时间，这让人有些沮丧。  

让我们看看reflect包中一共有多少个方法呢？

```go
reflect.Append()
reflect.Select()
reflect.AppendSlice()
reflect.ArrayOf()
reflect.ChanOf()
reflect.Copy()
reflect.DeepEqual()
reflect.FuncOf()
reflect.Indirect()
reflect.MakeChan()
reflect.MakeFunc()
reflect.MakeMap()
reflect.MakeSlice()
reflect.MapOf()
reflect.New()
reflect.NewAt()
reflect.PtrTo()
reflect.SliceOf()
reflect.StructOf()
reflect.Swapper()
reflect.ValueOf()
reflect.Zero()
```

哇！一共有22个方法，加上之前的typeof()是23个。没办法，既然别人能写得出来，我们也应该可以看得下来不是。

先从上向下看吧，第一个方法
`reflect.Append()`  
完整个的方法是结构是`func Append(s Value, x ...Value) Value {}`

先看一下它的注释：
```
// Append appends the values x to a slice s and returns the resulting slice.
// As in Go, each x's value must be assignable to the slice's element type.
```
把值X追加到切片s，并返回切片结果。在Go里面，每一个x的值必须被指派为切片元素类型。  
大概的意思似乎明白了，就是切片的合并。  
这样的话我写一段代码先试一下。  
```go
func main()  {
	
	slice := make([]string, 5)
	slice[0] = "Mon"
	slice[1] = "Tues"
	slice[2] = "Wed"
	slice[3] = "Thur"
	slice[4] = "Fri"

	sliceExt := make([]string, 2)
	sliceExt[0] = "Sat"
	sliceExt[1] = "sum"
	reflect.Append(slice,sliceExt)
	fmt.Println(slice)
}
```
第一次尝试，直接挂  
```
.\mian.go:33: cannot use slice (type []string) as type reflect.Value in argument to reflect.Append
.\mian.go:33: cannot use sliceExt (type []string) as type reflect.Value in argument to reflect.Append
```
经过调整，我发现两件事情。首先，传入reflect.Append()的两个值必须是Value类型。其次，是切片附加的操作，传入的第一个值是Slice类型，第二个则是其它类型（如int，string)，如果一来，我把方法再改了一下。  
```
func main()  {
	/*
	slice := make([]string, 5)
	slice[0] = "Mon"
	slice[1] = "Tues"
	slice[2] = "Wed"
	slice[3] = "Thur"
	slice[4] = "Fri"
	*/
	//为了简化，我改用下面的方式声明一个切片
	slice := []string{"Mon","Tues","Wed","Thur","Fri"}

	var newVal string = "sat"
	newSlice := reflect.Append(reflect.ValueOf(slice),reflect.ValueOf(newVal))
	fmt.Println(newSlice)
}
```
从方法中可以看到我用了一个reflect.ValueOf()的方法，将切片类型做了转换，转成了reflect.Append()要求的value类型。  
reflect.ValueOf()做了些什么？只能再到源代码中去翻。  

在上面的那个方法中，我将slice变量传入reflect.ValueOf(),而在reflect.ValueOf()中，将slice转成了原始类型interface{}

`*一切类型都可以变成interface{}类型`

接下来，在里面依次执行了escapes(i)和unpackEface(i)方法，并直接将unpackEface(i)方法作为返回值。  

看上去很简单。先看一下escapes(i)做了些什么吧？

这里我将main方法改造成了最简单的一个方法来进行测试：  
```go
func main()  {
	var newVal string = "hello"
	rs := reflect.ValueOf(newVal)
	fmt.Println(rs)
}
result:hello(什么都没有改变)
```

```
func escapes(x interface{}) {
	if dummy.b {
		dummy.x = x
	}
}

var dummy struct {
	b bool
	x interface{}
}
```
第一次调用了escapes(i)的方法，很明显dummy.b是false，因此，它什么都没有做，可以跳过。
`*dummy是复制品的意思，这里应该是一个克隆方法吧（猜）` 

那再看一下和unpackEface(i)方法吧。  
```go
func unpackEface(i interface{}) Value {
	e := (*emptyInterface)(unsafe.Pointer(&i))
	// NOTE: don't read e.word until we know whether it is really a pointer or not.
	t := e.typ
	if t == nil {
		return Value{}
	}
	f := flag(t.Kind())
	if ifaceIndir(t) {
		f |= flagIndir
	}
	return Value{t, e.word, f}
}
```
哇，看上去第一行就好眼熟啊，这是我们的老方法了，得到变量的信息。它主要为了获取e.typ和e.word两个数据。这里还有一个警告，让我不要读e.word直到我们确认他是否是指针。（什么鬼……）  
e.typ就是变量的信息主体了。再继续读下去，到flag(t.Kind())  
t.Kind()是得到变量的类型的数字编号，这里我得到的是24,即string  
flag其实是就是uintptr的别名，这里基本就是uintptr(24)的意思  
转了一下还是24啊。
然后又是ifaceIndir(t)，看注释上讲：
```
ifaceIndir reports whether t is stored indirectly in an interface value.
ifaceIndir报告t是否直接存在interface变量之中的
```
输出结果是true  
ifaceIndir()方法中执行的是  
`return t.kind&kindDirectIface == 0`
t.kind我知道的，是24，那kindDirectIface又是什么？  
在上面的常量定义中我看到：`kindDirectIface = 1 << 5`
`变量数据类型(1<<5)即为1左移5位，二进制即为 0010 0000`
