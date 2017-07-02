在go的reflect里面，我看到很多地方都用了unsafe.point方法，那么，这个unsafe.point到底是什么用处呢？
首先，我查看了一下unsafe包的源码，可惜里面除了声明，并没有实现的方法。
在声明中有注释：
```go
// Pointer represents a pointer to an arbitrary type.  There are four special operations
// available for type Pointer that are not available for other types.
//	1) A pointer value of any type can be converted to a Pointer.
//	2) A Pointer can be converted to a pointer value of any type.
//	3) A uintptr can be converted to a Pointer.
//	4) A Pointer can be converted to a uintptr.
// Pointer therefore allows a program to defeat the type system and read and write
// arbitrary memory. It should be used with extreme care.
type Pointer *ArbitraryType
```
用我拙劣的英文翻译了一下  
指针以任意一种类型描述成一个新的指针，一共有四种特别的操作  
1.一个任意类型的指针值能被换化成一个指针  
2.一个指针能被转换成一个任意类型的指针值  
3.一个uintptr能被转换成一个指针  
4.一个指针能被转换成一个uintptr  

`uintptr：专门用于存储内存地址的类型`  
