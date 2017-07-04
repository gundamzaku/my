
在reflect包中，定义了一组常量
```go
type Kind uint
const (
	Invalid Kind = iota
	Bool
	Int
	Int8
	Int16
	Int32
	Int64
	Uint
	Uint8
	Uint16
	Uint32
	Uint64
	Uintptr
	Float32
	Float64
	Complex64
	Complex128
	Array
	Chan
	Func
	Interface
	Map
	Ptr
	Slice
	String
	Struct
	UnsafePointer
)
```
这组常量都是Kind类型（即uint类型），iota值为0，这个是在builtin包中定义的一个常量  
`builtin包是go的预声明定义,包括go语言中常用的各种类型和方法声明,包括变量和常量两部分.`  
`const iota = 0 // Untyped int.`  
按照go语言特殊的定义，从Invalid向下，就是不停的++的过程，Invalid为0，Bool为1，Int为2……以此类推。  
可是我在`fmt.Println(reflect.Int)`的时候，显示的result为`int`，而不是数字，这是怎么回事？
问题出在下面一段代码的定义上面
```go
var kindNames = []string{
	Invalid:       "invalid",
	Bool:          "bool",
	Int:           "int",
	Int8:          "int8",
	Int16:         "int16",
	Int32:         "int32",
	Int64:         "int64",
	Uint:          "uint",
	Uint8:         "uint8",
	Uint16:        "uint16",
	Uint32:        "uint32",
	Uint64:        "uint64",
	Uintptr:       "uintptr",
	Float32:       "float32",
	Float64:       "float64",
	Complex64:     "complex64",
	Complex128:    "complex128",
	Array:         "array",
	Chan:          "chan",
	Func:          "func",
	Interface:     "interface",
	Map:           "map",
	Ptr:           "ptr",
	Slice:         "slice",
	String:        "string",
	Struct:        "struct",
	UnsafePointer: "unsafe.Pointer",
}
```
在value.go的文件里面，go将kindNames和最上面的常量串在了一起。只是单纯的定义了这个kindNames并没有实际的意思
```go
func (k Kind) String() string {
	if int(k) < len(kindNames) {
		return kindNames[k]
	}
	return "kind" + strconv.Itoa(int(k))
}
```
真正将两者串起来的是这个String()的隐函数。之所以称之为隐函数，是因为它控制了fmt.println()
我现在`fmt.println(Int8)`，实际上是传了一个值8到String()里面去，代码判定8小于kindNames的总长度，因此，将`Uint8:"uint8"`返回
如果我传一个超长的值，const (UnsafePointer)后面我再加一个常量如Unknow，这个常量在KindNames中并没有，然后再试着println  
`result:kind27`,解发了`return "kind" + strconv.Itoa(int(k))`的方法

