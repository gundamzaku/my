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
