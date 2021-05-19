# printf底层调用分析

对于编译型语言，程序的运行需要经过预编译、编译、汇编和链接四个步骤。接下来以printf函数为例，分别使用动态GDB调试和静态源码分析获取其底层实现流程。

测试环境为：


测试代码如下：
```c
#include <stdio.h>

int main()
{
    printf("Hello, world!\n");
    return 0;
}
```



![printf动态调用流程](images/printfGDB.svg)



![printf静态代码分析](images/printfCODE.svg)


## 参考链接：
[printf背后的故事](https://www.cnblogs.com/fanzhidongyzby/p/3519838.html) <br>
[I/O设备管理实验 - 代码分析](http://edward-zhu.github.io/special/os_exp/2015/01/03/exp-6.2.html)
