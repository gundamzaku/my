GO中的包
type.go
reflect.TypeOf方法
```
var i int = 123
fmt.Println(reflect.TypeOf(i))
```
出来的结果是`int`

看一下源代码做了什么操作
```go
func TypeOf(i interface{}) Type {
	eface := *(*emptyInterface)(unsafe.Pointer(&i))
	return toType(eface.typ)
}
```
首先传入的是一个interface{},空interface(interface{})不包含任何的method，正因为如此，所有的类型都实现了空interface。  
顺着这一点，我决定新建一个包，将reflect包中的文件精简出来，看一下TypeOf到底是怎么样运作的。  
在reflact包中，最最重要的就是type.go和value.go两个文件。  
现在我新建一个新的包，命名为selfReflact包，并新建一个type.go文件。  

通过TypeOf，我扒出了另外一个方法toType，然后又找到emptyInterface的结构，具体的精简代码可以参考我的go文件，此不复述。
值得注意的是unsafe.Pointer()这个方法，这是go的另外一个包unsafe里的内容，在这里不做深入，仅了解它的意思。
顾名思义，这是一个不安全的方法，他在此处的功能就是强制进行指针类型的转换，而这在平时的go语言中是不被允许的，前面看过一篇文章，是讲unsafe这个包的不实用性，实际上可以看出，在go语言包库中还是有一定用处的。
了解到这一点以后，就可以看出，上面的语句就是把我们传进来的i这个变量的地址强行转成了emptyInterface结构并做成了一个指针对象。

```go
type emptyInterface struct {
	typ  *rtype
	word unsafe.Pointer
}
```
emptyInterface由typ和word两个元素组成，word是一个unsafe.Pointer类型，目前他到底代表什么意思？我不得而知。
而typ则是一个rtype的结构

```go
type rtype struct {
	size          uintptr
	ptrdata       uintptr
	hash          uint32         // hash of type; avoids computation in hash tables
	alg           *typeAlg       // algorithm table
	gcdata        *byte          // garbage collection data
	string        *string        // string form; unnecessary but undeniably useful
	*uncommonType                // (relatively) uncommon fields
	kind          uint8

}
```
在rtype又有一个uncommonType的结构体
```go
type uncommonType struct {
	name    *string  // name of type
	pkgPath *string  // import path; nil for built-in types like int, string
	methods []method // methods associated with type
}
```
这一来一去，事情就变得复杂了。他们到底代表什么意思？虽然源码中还有英文的注释，但是究竟他们之间是如何运作起来的，我还是不清楚。
目前可以肯定的是`eface := *(*emptyInterface)(unsafe.Pointer(&i))`这段代码执行以后。
现在fmt.println(eface.uncommonType.name)`(eface.name)`也可以，他会自动跳过uncommonType，形成一个缩写。
我决定单独试一下这段代码
现在再进行抽象
