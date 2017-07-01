GO中的包
type.go
reflect.TypeOf方法
```
var i int = 123
fmt.Println(reflect.TypeOf(i))
```
出来的结果是`int`

看一下源代码做了什么操作
```
func TypeOf(i interface{}) Type {
	eface := *(*emptyInterface)(unsafe.Pointer(&i))
	return toType(eface.typ)
}
```
首先传入的是一个interface{},空interface(interface{})不包含任何的method，正因为如此，所有的类型都实现了空interface。
顺着这一点，我决定新建一个包，将reflect包中的文件精简出来，看一下TypeOf到底是怎么样运作的。
在reflact包中，最最重要的就是type.go和value.go两个文件。
现在我新建一个新的包，命名为selfReflact包，并新建一个type.go文件。
