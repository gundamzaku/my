看uintptr前，先看一段C代码

```c
#include <stdio.h>

int main() {
    void *vp;
    int val = 100;
    int *p;
    *p = val;
    vp = p;
    printf("%d",*(int *)vp);
    return 0;
}
```
在这段代码中，已经产生了3个变量。   
一个是void类型的指针vp  
一个是int类型的变量val，值为100  
一个是int类型的指针p  
然后让指针p指到val的地址，再把指针p赋给了vp。  
由此可见，`void*`就是一个万能指针类型，任何指针都可以赋值给它。那么方法可以么？  

```c
#include <stdio.h>

void * getVal(void * vp){
    printf("hello\n");
    return vp;
}

int main() {

    int i =  100;
    int *pi;
    *pi = i;
    void* rs = getVal(pi);
    printf("%d",*(int *)rs);
    return 0;
}
```

```c
#include <stdio.h>

void * getVal(void * vp){
    printf("hello\n");
    return vp;
}

int main() {

    char *c;
    c = "a";
    void * rs = getVal(c);
    printf("%c",*(char *)rs);
    return 0;
}
```
从上面两段代码我们可以看出来，同样的函数，可以传入不同类型的变量，再也没有对变量类型的约束。
这样一来，似乎就可以衍生出很多有意思的写法了。

不过在这里就此打住，毕竟现在在学的是Go语言，我再回过来看uintptr，
在Go的源代码中是这么定义uintptr的
`typedef uint64          uintptr;`
由此可见，unitptr就是一个整型，那么它是干什么的呢？
网上找到一句话：uintptr主要用于golang中的指针运算。看来是和指针有关系，而更进一步的说法是，uintptr存放指针地址的整形
