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
