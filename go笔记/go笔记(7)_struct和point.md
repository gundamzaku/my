经过上一篇学习的惨痛失败，这次我将目标压缩在最小的范围之内。  

首先先看一段最简单的代码：  

```go
type dan struct{
	name string
	age int
}

func main()  {
	var student dan;
	student = dan{"dan",20}
	fmt.Println(student)
}
```
创建一个结构体dan，然后赋值。  
接下来，我试着把它改造成一个指针的形式。  
