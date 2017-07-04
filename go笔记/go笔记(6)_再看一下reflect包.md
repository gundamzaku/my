
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
`const iota = 0 // Untyped int.`  
按照go语言特殊的定义，从Invalid向下，就是不停的++的过程，Invalid为0，Bool为1，Int为2……以此类推。  
