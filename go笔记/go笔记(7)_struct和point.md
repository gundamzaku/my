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
